---
layout: post
title:  "🤖🖼 Twitterbot med konstverk från Digitalt museum"
date:   2020-03-01 12:00:00 +0100
tags: [Open Source, Javascript, Collections]
author: Aron Ambrosiani
---
I fredags knåpade jag ihop en twitterbot som en gång om dagen twittrar ett konstverk av Fritz von Dardel (1817–1901). Tänkte berätta hur jag gjorde så att det blir enklare för nästa person som vill bygga en twitterbot med konstverk hämtade från Digitalt museum.

## Från idé till twitterbot i fem (någorlunda) enkla steg!
1. Skapa twitterkonto och twitterapp
2. Kopiera kod på Glitch
3. Hämta data från Digitalt museum
4. Ställ in ett cronjob
5. Luta dig tillbaka och njut av konst i twitterflödet!

## 1. Skapa twitterkonto och twitterapp
Sajten [🤖 Botwiki.org](https://botwiki.org) har en hel del matnyttigt för den som vill bygga bottar (olika sorters hel- eller halvautomatiserade konton på sociala medier). Följ guiden [How to create a Twitter app](https://botwiki.org/resource/tutorial/how-to-create-a-twitter-app/) tills du har twitterkonto, utvecklarkonto och en registerad app.

## 2. Kopiera kod på Glitch
Sajten [🎏 Glitch](http://glitch.com) är en blandning av kodbibliotek och webbhotell, där den kod du skriver byggs och körs i realtid. Det är dessutom väldigt enkelt att remixa (dvs kopiera och ändra) någon annans kod. Och det är precis vad vi ska göra!

Jag har remixat ett ["starter kit" för twitterbotar](https://glitch.com/~twitterbot) och gjort några anpassningar, så det är bättre att utgå från den färdiga boten [Fritz von Dardel](https://glitch.com/~fritzvondardel). Följ länken, leta rätt på ”remix”-knappen och klistra sedan in dina twitterappuppgifter i filen som heter **.env** (se guiden ”How to create a Twitter app” ovan).

## 3. Hämta data från Digitalt museum
*Den här delen av guiden kommer att uppdateras när jag hunnit få lite återkoppling från KulturIT.*

Istället för att anropa Digitalt museum varje gång boten ska twittra har jag laddat hem data med hjälp av Digitalt museums API. Det innebär att eventuella ändringar i samlingsposterna inte slår igenom förrän jag upprepar API-anropet.

Jag har använt följande anrop: `http://api.dimu.org/api/solr/select?q=*&fq=identifier.owner:S-NM&fq=artifact.type:Photograph&fq=artifact.producer:Dardel&wt=json&rows=100&api.key=demo`.

Anropet frågar efter fotografier i Nordiska museets samlingar där fältet `artifact.producer` innehåller ”Dardel”. Detta kommer att bytas ut mot ett anrop med Kulturanv-UUID när jag vet hur man gör!

Får att få fler än 10 svar tillbaka behöver du en egen API-nyckel till Digitalt museum (istället för ”demo” sist i anropet). Kontakta KulturIT för att få en nyckel.

Den data jag fick tillbaka har jag sparat i filen `data.json` (och plockat bort min API-nyckel).

För att hämta bildfilerna har jag…
1. avkommenterat rad 4–8 i `server.js` & kopierat texten från konsollen
2. öppnat Glitchappens terminal (finns under knappen ”Tools”)
3. i mappen images kört den radda wget-kommandon som genererades i steg 1
4. avkommenterat rad 10–14 i `server.js` & kopierat texten från konsollen
5. i mappen images kört den radda wget-kommandon som genererades i steg 4

Nu är data, bildfiler och kod på plats och du kan börja twittra!

## 4. Ställ in ett cronjob
På sajten [Cron-job.org](https://cron-job.org/en/) har jag ställt in ett cronjob som körs en gång om dagen och anropar den endpoint som anges i glitchappens .env-fil, dvs https://fritzvondardel.glitch.me/ENDPOINT (där du byter ut sista delen mot din egen endpoint). Appen har ingen autentisering så om någon annan listar ut din endpoint kan de twittra för fulla muggar!

## 5. Luta dig tillbaka och njut av konst i twitterflödet!
<blockquote class="twitter-tweet" data-dnt="true" data-theme="light"><p lang="sv" dir="ltr">Exteriörmiljö från ett halländskt gästgiveri, till vänster: en betalande resenär. Teckning av Fr. v. Dardel (1817-1901) ur: &quot;Mrs. Black&amp;Smith. En route pour la Scandinavie&quot;. Handskrift.<a href="https://t.co/90PTM9Xu3p">https://t.co/90PTM9Xu3p</a> <a href="https://t.co/zqtbGl3V44">pic.twitter.com/zqtbGl3V44</a></p>&mdash; Fritz von Dardel (@FritzVonDardel) <a href="https://twitter.com/FritzVonDardel/status/1233755054554910720?ref_src=twsrc%5Etfw">February 29, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
