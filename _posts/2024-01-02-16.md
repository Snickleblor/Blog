---
layout: post
title: A simple way to add one to one chat between users in Django using Pusher API
date: 2024-01-02
author: Simon
categories: programmering 
---

```python
"""
path: direct/t/<int:receiver_id>

Logic:
User with id of 0 goes to direct/t/1 to talk to User with id of 1
User with id of 0 makes post request to direct/t/1 
    direct/t/1 pub message to private-chat-0-to-1
    User with id of 1 is subscribed to private-chat-0-to-1 
    User with id of 1 sees the message, including User with id of 0

Vica versa...
"""
from django.contrib.auth.decorators import login_required
from django.shortcuts import render, get_object_or_404
from django.http import JsonResponse


"""
If you were to change the model in the near future, then this would not break the application.
Retrieving it by get_user_model() is therefore better practice; hence we do this here.
"""
from django.contrib.auth import get_user_model

User = get_user_model() 

@login_required 
def direct_chat(request, receiver_id):
    receiver_user = get_object_or_404(User, id=receiver_id)

    form = ChatForm() # Assuming you have a ChatForm() 

    if request.method == 'POST':
        form = ChatForm(request.POST) 
        if form.is_valid():
            """
            The initiator will publish a message to the channel that the receiver 
            is subscribed to on the client side and the client will therefore
            see the message 
            """
            if request.user.id > receiver_id:
                channel_name = f'chat-{request.user.id}-to-{receiver_id}'
            else:
                channel_name = f'chat-{receiver_id}-to-{request.user.id}'

            pusher_client.trigger(channel_name, 'message', {'user': request.user.username, 'message': form.cleaned_data['message']})

    context = {
        'initiator_id': request.user.id,
        'receiver_id': receiver_id,
        'receiver_user': receiver_user,
        'form': form,
    }

    return render(request, 'chat/direct_chat.html', context)
```

```html
<h1>Private Chat with {% raw %}{{ receiver_user.username }} {% endraw%}</h1>
<h1>chat-{% raw %}{{initiator_id}} {% endraw%}-to-{% raw %}{{receiver_id}} {% endraw %}</h1>

{#
Pipe the initiator_id and receiver_id from context as json_script
to then retrieve it on the Javascript side. 

Another way to do this is to mix the Javascript and Django templating.
But it is better practice to keep the logic seperate...
#}

{% raw %}
{{ initiator_id|json_script:"initiator_id" }}
{{ receiver_id|json_script:"receiver_id" }}
{% endraw %}

<script src="https://js.pusher.com/8.2.0/pusher.min.js"></script>

<div id="messageList"></div>

<form action="{% raw %}{% url 'direct_chat' receiver_id %}{% endraw %}" method="POST" id="private-chat">
    {% raw %}
    {% csrf_token %} 
    {{ form.as_p }}
    {% endraw %}
    <input type="submit">
</form>

<script>
  Pusher.logToConsole = true;

  const csrf_token = document.querySelector('input[name="csrfmiddlewaretoken"]').value;

  const initiator_id = JSON.parse(document.getElementById('initiator_id').textContent);
  const receiver_id = JSON.parse(document.getElementById('receiver_id').textContent);

  var pusher = new Pusher('aab3125d8668c3af08b4', {
    cluster: 'eu'
  });

  <!-- 
  The same logic from the view is implemented here...
  -->
  if (initiator_id > receiver_id) {
    var channel_name = `chat-${initiator_id}-to-${receiver_id}`;
  } else {
    var channel_name = `chat-${receiver_id}-to-${initiator_id}`;
  };

  const channel = pusher.subscribe(channel_name);

  channel.bind('message', data => {
    const createMessage = (user, message) => {
      const p = document.createElement('p');
      p.textContent = `${user}: ${message}`;
      return p;
    };

    const messageEl = document.querySelector('#messageList');
    messageEl.appendChild(createMessage(data.user, data.message));
  });

  const form = document.querySelector('#private-chat');
  form.addEventListener('submit', event => {
    <!-- 
    Preventing the default form behavior and doing it explicity by fetch API 
    The fetch API makes a post request with the form information, and the view handles the post request.
    -->
    event.preventDefault(); 

    const formData = new FormData(form);
    fetch(form.action, {
      method: form.method,
      headers:{ 'X-CSRFToken': csrf_token },
      body: formData,
    }).then(response => console.log(response))

  });
</script>
```
