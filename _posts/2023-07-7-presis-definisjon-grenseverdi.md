---
layout: post
title: Epsilondelta definisjon av grenseverdi
date: 2023-07-7
author: Simon
categories: Matematikk
---
Vi har lært om den intuitive definisjonen av en grenseverdi fra tidligere. Likevel, så forteller dette oss veldig lite over hva en grenseverdi faktisk "sier". I denne bloggen, så ønsker jeg å gjøre dette mer tydelig.

La $$f(x)$$ være en vilkårlig funksjon, f.eks, 

$$ f(x) = 2x - 1 $$

Dersom vi ønsker å beregne grenseverdien for denne funksjonen, hvor $$x$$ går mot $$3$$, så er det så klart tydelig at dette blir

$$ \lim_{x \to 3} \, f(x) = 2(3) - 1 = 5 $$

Men, nærheten mellom $$x$$ og $$3$$, og hvorledes $$f(x)$$ tilnærmer seg $$L$$, er uklart og upresist. En grenseverdi beskriver en subtil endring mellom to verdier, og denne endringen har en direkte korrelasjon med to andre verdier, nemlig y-verdiene. For å forstå nøyaktig hvorledes $$f(x)$$ endrer seg når $$x$$ nærmer seg $$3$$, må vi stille oss følgende spørsmål:

> Hvor nærme $$3$$ må $$x$$ være for at $$f(x)$$ skildres fra $$5$$ med mindre enn $$0.1$$?

Vi vet at distansen mellom $$x$$ til $$3$$ er definert som $$ \mid x - 3 \mid $$ og at distansen fra $$f(x)$$ til $$5$$ er $$ \mid f(x) - 5 \mid $$. Vi må således finne ut et tall $$\delta$$ delta slik at,

$$ \mid f(x) - 5 \mid  < 0.1 \quad \text{hvis} \quad \mid x - 3 \mid  < \delta $$

Hvis $$ \mid x - 3 \mid  > 0$$ så kan vi omformulere det slik,

$$ \mid f(x) - 5 \mid  < 0.1 \quad \text{hvis} \quad 0 <  \mid x - 3 \mid  < \delta $$

Merk deg at hvis,

$$ 0 <  \mid x - 3 \mid  < (0.1)/2 = 0.05 $$

så er,

$$ 
\mid f(x) - 5 \mid = \mid (2x - 1) - 5 \mid \\
\mid 2x - 6 \mid  = 2 \mid x - 3 \mid  < 2(0.05) = 0.1 
$$

Det betyr at, 

$$ \mid f(x) - 5 \mid  < 0.1 \quad \text{hvis} \quad 0 <  \mid x - 3 \mid  < 0.05 $$

Og som du ser, har vi således besvart problemstillingen vår.

Vi ser tydelig at $$\delta = 0.05$$, hvis $$x$$ er mellom $$0.05$$ og $$3$$, som vil si at $$f(x)$$ vil være mellom $$0.1$$ og $$5$$

Klart nok, hvis vi forandret tallet $$0.1$$ til et mindre tall som $$0.01$$; og ved å bruke den samme metoden, så vil 

$$ \delta = (0.01)/2 = 0.005 $$

Dersom vi velger et mindre og mindre tall- mer presis vil vi være. Vi kan se på de tallene vi velger, $$0.1$$ og $$0.01$$ som akseptabel avvik. For at denne grenseverdien skal være presis, så kan vi ikke bare bringe differansen mellom $$f(x)$$ og $$5$$  under hvert av disse to tallene. Vi må gjøre dette her for hvert positivt tall, $$\mathbb{N}^{+}$$

Så i stedet for å velge verdier som $$0.1$$ og $$0.01$$ så kan vi formulere det slik:

La tallet $$\epsilon$$ være et positivt tall. 

således så er,

$$ \mid f(x) - 5 \mid  < \epsilon \quad \text{hvis} \quad 0 <  \mid x - 3 \mid  < \delta = \epsilon/2$$

Dette er en presis definisjon av en grenseverdi fordi vi kan lage verdiene av $$f(x)$$ mellom en distanse $$\epsilon$$ og $$5$$ med å begrense verdiene av $$x$$ til å være mellom $$\epsilon/2$$ fra $$3$$

Vi kan deretter formulere det slik:

> La $$f(x)$$ være en funksjon definert på en åpent interval sånn at det inneholder et tall $$a$$, kanskje muligens på $$a$$ dets selv. Deretter kan vi si at grenseverdien av $$f(x)$$ når $$a$$ nærmer seg $$a$$ er $$L$$, og vi skriver 
> $$\lim_{x \to a} \, f(x) = L$$
> Hvis for hvert tall $$\epsilon > 0$$ så er det et tall $$\delta > 0$$ slik at
> Hvis $$0 <  \mid x - a \mid  < \delta$$ så er $$ \mid f(x) - L \mid  < \epsilon$$

I ord så kan vi si at grenseverdien til funksjonen $$f$$ når $$x$$ nærmer seg $$a$$ betyr at distansen mellom $$f$$ og $$L$$ kan gjøres om til et lite tall med at distansen fra $$x$$ til $$a$$ er liten også, men ikke eksakt 0.
