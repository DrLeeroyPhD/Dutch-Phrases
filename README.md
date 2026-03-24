<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>530 Essential Dutch Sentences</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #f5f4f0; color: #1a1a18; line-height: 1.6; }
  header { background: #fff; border-bottom: 1px solid #e2e0d8; padding: 1.5rem 2rem; position: sticky; top: 0; z-index: 100; }
  header h1 { font-size: 1.4rem; font-weight: 600; color: #1a1a18; margin-bottom: 0.75rem; }
  header p { font-size: 0.85rem; color: #6b6b68; margin-bottom: 1rem; }
  .controls { display: flex; gap: 10px; flex-wrap: wrap; }
  input[type="search"] { flex: 1; min-width: 200px; padding: 8px 14px; border: 1px solid #d0cec6; border-radius: 8px; font-size: 14px; background: #fafaf8; outline: none; }
  input[type="search"]:focus { border-color: #534AB7; }
  select { padding: 8px 14px; border: 1px solid #d0cec6; border-radius: 8px; font-size: 14px; background: #fafaf8; cursor: pointer; }
  .stats { font-size: 0.8rem; color: #888; margin-top: 0.5rem; }
  main { max-width: 960px; margin: 0 auto; padding: 1.5rem 1rem 3rem; }
  .category-header { font-size: 1rem; font-weight: 600; color: #534AB7; margin: 1.5rem 0 0.75rem; padding: 0.5rem 0; border-bottom: 2px solid #EEEDFE; display: flex; align-items: center; gap: 8px; }
  .category-icon { font-size: 1.1rem; }
  .sentence-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 10px; }
  .card { background: #fff; border: 1px solid #e2e0d8; border-radius: 10px; padding: 0.85rem 1rem; cursor: pointer; transition: border-color 0.15s; }
  .card:hover { border-color: #AFA9EC; }
  .card .nl { font-size: 0.95rem; font-weight: 500; color: #1a1a18; margin-bottom: 3px; }
  .card .en { font-size: 0.82rem; color: #6b6b68; }
  .card .num { font-size: 0.7rem; color: #b0aead; float: right; }
  .no-results { text-align: center; padding: 3rem; color: #888; font-size: 0.95rem; }
  .cat-badge { display: inline-block; font-size: 0.7rem; background: #EEEDFE; color: #534AB7; border-radius: 5px; padding: 1px 6px; margin-left: 6px; font-weight: 500; }
  @media print { header { position: static; } .controls { display: none; } }
</style>
</head>
<body>

<header>
  <h1>🇳🇱 530 Essential Dutch Sentences</h1>
  <p>Daily-life Dutch for living in the Netherlands — search, filter, and study at your own pace.</p>
  <div class="controls">
    <input type="search" id="search" placeholder="Search Dutch or English..." oninput="filter()">
    <select id="catFilter" onchange="filter()">
      <option value="">All categories</option>
    </select>
  </div>
  <div class="stats" id="stats"></div>
</header>

<main id="main"></main>

<script>
const data = [
  // ===== GREETINGS & FAREWELLS (1–30) =====
  { id:1,  cat:"Greetings & Farewells", nl:"Goedemorgen!", en:"Good morning!" },
  { id:2,  cat:"Greetings & Farewells", nl:"Goedemiddag!", en:"Good afternoon!" },
  { id:3,  cat:"Greetings & Farewells", nl:"Goedenavond!", en:"Good evening!" },
  { id:4,  cat:"Greetings & Farewells", nl:"Hallo, hoe gaat het?", en:"Hello, how are you?" },
  { id:5,  cat:"Greetings & Farewells", nl:"Het gaat goed, dank je.", en:"I'm doing well, thank you." },
  { id:6,  cat:"Greetings & Farewells", nl:"Niet zo goed, helaas.", en:"Not so good, unfortunately." },
  { id:7,  cat:"Greetings & Farewells", nl:"Hoe gaat het met jou?", en:"How are you doing?" },
  { id:8,  cat:"Greetings & Farewells", nl:"Dag!", en:"Bye! / Hello! (informal)" },
  { id:9,  cat:"Greetings & Farewells", nl:"Doei!", en:"Bye! (very casual)" },
  { id:10, cat:"Greetings & Farewells", nl:"Tot ziens!", en:"Goodbye! / See you!" },
  { id:11, cat:"Greetings & Farewells", nl:"Tot morgen!", en:"See you tomorrow!" },
  { id:12, cat:"Greetings & Farewells", nl:"Tot straks!", en:"See you later!" },
  { id:13, cat:"Greetings & Farewells", nl:"Welkom!", en:"Welcome!" },
  { id:14, cat:"Greetings & Farewells", nl:"Fijne dag!", en:"Have a nice day!" },
  { id:15, cat:"Greetings & Farewells", nl:"Fijn weekend!", en:"Have a nice weekend!" },
  { id:16, cat:"Greetings & Farewells", nl:"Goed nacht!", en:"Good night!" },
  { id:17, cat:"Greetings & Farewells", nl:"Prettige vakantie!", en:"Have a nice holiday!" },
  { id:18, cat:"Greetings & Farewells", nl:"Gefeliciteerd!", en:"Congratulations!" },
  { id:19, cat:"Greetings & Farewells", nl:"Van harte gefeliciteerd!", en:"Heartfelt congratulations!" },
  { id:20, cat:"Greetings & Farewells", nl:"Proost!", en:"Cheers!" },
  { id:21, cat:"Greetings & Farewells", nl:"Eet smakelijk!", en:"Enjoy your meal!" },
  { id:22, cat:"Greetings & Farewells", nl:"Hoi, alles goed?", en:"Hi, everything alright?" },
  { id:23, cat:"Greetings & Farewells", nl:"Prima, jij ook?", en:"Great, you too?" },
  { id:24, cat:"Greetings & Farewells", nl:"Prettig kennis te maken.", en:"Nice to meet you." },
  { id:25, cat:"Greetings & Farewells", nl:"Aangenaam.", en:"Pleased to meet you." },
  { id:26, cat:"Greetings & Farewells", nl:"Leuk je te zien!", en:"Nice to see you!" },
  { id:27, cat:"Greetings & Farewells", nl:"Lang niet gezien!", en:"Long time no see!" },
  { id:28, cat:"Greetings & Farewells", nl:"Fijne avond!", en:"Have a nice evening!" },
  { id:29, cat:"Greetings & Farewells", nl:"Sterkte!", en:"Good luck / Stay strong!" },
  { id:30, cat:"Greetings & Farewells", nl:"Succes!", en:"Good luck!" },

  // ===== INTRODUCTIONS (31–50) =====
  { id:31, cat:"Introductions", nl:"Ik heet [naam].", en:"My name is [name]." },
  { id:32, cat:"Introductions", nl:"Hoe heet jij?", en:"What is your name?" },
  { id:33, cat:"Introductions", nl:"Waar kom jij vandaan?", en:"Where are you from?" },
  { id:34, cat:"Introductions", nl:"Ik kom uit [land].", en:"I come from [country]." },
  { id:35, cat:"Introductions", nl:"Ik woon in Amsterdam.", en:"I live in Amsterdam." },
  { id:36, cat:"Introductions", nl:"Hoe oud ben jij?", en:"How old are you?" },
  { id:37, cat:"Introductions", nl:"Ik ben [getal] jaar oud.", en:"I am [number] years old." },
  { id:38, cat:"Introductions", nl:"Wat doe je voor werk?", en:"What do you do for work?" },
  { id:39, cat:"Introductions", nl:"Ik werk als [beroep].", en:"I work as a [profession]." },
  { id:40, cat:"Introductions", nl:"Ik studeer aan de universiteit.", en:"I study at university." },
  { id:41, cat:"Introductions", nl:"Spreek je Engels?", en:"Do you speak English?" },
  { id:42, cat:"Introductions", nl:"Ik leer Nederlands.", en:"I am learning Dutch." },
  { id:43, cat:"Introductions", nl:"Mijn Nederlands is nog niet zo goed.", en:"My Dutch is not that good yet." },
  { id:44, cat:"Introductions", nl:"Spreek je een beetje langzamer?", en:"Can you speak a little slower?" },
  { id:45, cat:"Introductions", nl:"Ik woon hier pas kort.", en:"I have only lived here a short time." },
  { id:46, cat:"Introductions", nl:"Ik ben getrouwd.", en:"I am married." },
  { id:47, cat:"Introductions", nl:"Ik heb twee kinderen.", en:"I have two children." },
  { id:48, cat:"Introductions", nl:"Dit is mijn man / vrouw.", en:"This is my husband / wife." },
  { id:49, cat:"Introductions", nl:"Ik ben hier voor mijn werk.", en:"I am here for my work." },
  { id:50, cat:"Introductions", nl:"Mijn telefoonnummer is...", en:"My phone number is..." },

  // ===== BASIC PHRASES & POLITE EXPRESSIONS (51–75) =====
  { id:51, cat:"Basic Phrases", nl:"Ja.", en:"Yes." },
  { id:52, cat:"Basic Phrases", nl:"Nee.", en:"No." },
  { id:53, cat:"Basic Phrases", nl:"Alsjeblieft.", en:"Please. / Here you go. (informal)" },
  { id:54, cat:"Basic Phrases", nl:"Dank je wel.", en:"Thank you. (informal)" },
  { id:55, cat:"Basic Phrases", nl:"Dank u wel.", en:"Thank you. (formal)" },
  { id:56, cat:"Basic Phrases", nl:"Heel erg bedankt!", en:"Thank you very much!" },
  { id:57, cat:"Basic Phrases", nl:"Graag gedaan.", en:"You're welcome." },
  { id:58, cat:"Basic Phrases", nl:"Geen probleem.", en:"No problem." },
  { id:59, cat:"Basic Phrases", nl:"Sorry.", en:"Sorry." },
  { id:60, cat:"Basic Phrases", nl:"Pardon!", en:"Excuse me! / Sorry!" },
  { id:61, cat:"Basic Phrases", nl:"Het spijt me.", en:"I am sorry." },
  { id:62, cat:"Basic Phrases", nl:"Maakt niet uit.", en:"Never mind / It doesn't matter." },
  { id:63, cat:"Basic Phrases", nl:"Weet je het niet?", en:"Don't you know?" },
  { id:64, cat:"Basic Phrases", nl:"Ik weet het niet.", en:"I don't know." },
  { id:65, cat:"Basic Phrases", nl:"Ik begrijp het niet.", en:"I don't understand." },
  { id:66, cat:"Basic Phrases", nl:"Kunt u dat herhalen?", en:"Can you repeat that?" },
  { id:67, cat:"Basic Phrases", nl:"Wat betekent dat?", en:"What does that mean?" },
  { id:68, cat:"Basic Phrases", nl:"Hoe zeg je ... in het Nederlands?", en:"How do you say ... in Dutch?" },
  { id:69, cat:"Basic Phrases", nl:"Kun je het opschrijven?", en:"Can you write it down?" },
  { id:70, cat:"Basic Phrases", nl:"Natuurlijk!", en:"Of course!" },
  { id:71, cat:"Basic Phrases", nl:"Misschien.", en:"Maybe." },
  { id:72, cat:"Basic Phrases", nl:"Zeker weten!", en:"Absolutely! / For sure!" },
  { id:73, cat:"Basic Phrases", nl:"Klopt!", en:"That's right! / Correct!" },
  { id:74, cat:"Basic Phrases", nl:"Oké.", en:"Okay." },
  { id:75, cat:"Basic Phrases", nl:"Doe maar.", en:"Go ahead / Just do it." },

  // ===== QUESTIONS (76–100) =====
  { id:76,  cat:"Questions", nl:"Wat?", en:"What?" },
  { id:77,  cat:"Questions", nl:"Wie?", en:"Who?" },
  { id:78,  cat:"Questions", nl:"Waar?", en:"Where?" },
  { id:79,  cat:"Questions", nl:"Wanneer?", en:"When?" },
  { id:80,  cat:"Questions", nl:"Waarom?", en:"Why?" },
  { id:81,  cat:"Questions", nl:"Hoe?", en:"How?" },
  { id:82,  cat:"Questions", nl:"Hoeveel kost dit?", en:"How much does this cost?" },
  { id:83,  cat:"Questions", nl:"Hoe laat is het?", en:"What time is it?" },
  { id:84,  cat:"Questions", nl:"Hoe ver is het?", en:"How far is it?" },
  { id:85,  cat:"Questions", nl:"Is er een [winkel] in de buurt?", en:"Is there a [shop] nearby?" },
  { id:86,  cat:"Questions", nl:"Kunt u mij helpen?", en:"Can you help me?" },
  { id:87,  cat:"Questions", nl:"Waar is het toilet?", en:"Where is the toilet?" },
  { id:88,  cat:"Questions", nl:"Mag ik de rekening?", en:"Can I have the bill?" },
  { id:89,  cat:"Questions", nl:"Wanneer gaat de winkel open?", en:"When does the shop open?" },
  { id:90,  cat:"Questions", nl:"Hoe kom ik bij...?", en:"How do I get to...?" },
  { id:91,  cat:"Questions", nl:"Is dit de goede weg naar...?", en:"Is this the right way to...?" },
  { id:92,  cat:"Questions", nl:"Heeft u dit in een andere maat?", en:"Do you have this in another size?" },
  { id:93,  cat:"Questions", nl:"Wat raadt u aan?", en:"What do you recommend?" },
  { id:94,  cat:"Questions", nl:"Kunt u een taxi bellen?", en:"Can you call a taxi?" },
  { id:95,  cat:"Questions", nl:"Welk platform vertrekt de trein?", en:"Which platform does the train depart from?" },
  { id:96,  cat:"Questions", nl:"Is er wifi hier?", en:"Is there wifi here?" },
  { id:97,  cat:"Questions", nl:"Zijn er nog plaatsen vrij?", en:"Are there still seats available?" },
  { id:98,  cat:"Questions", nl:"Wanneer is de volgende bus?", en:"When is the next bus?" },
  { id:99,  cat:"Questions", nl:"Heeft u een kamer vrij?", en:"Do you have a room available?" },
  { id:100, cat:"Questions", nl:"Wat zijn de openingstijden?", en:"What are the opening hours?" },

  // ===== TIME & DATES (101–120) =====
  { id:101, cat:"Time & Dates", nl:"Het is drie uur.", en:"It is three o'clock." },
  { id:102, cat:"Time & Dates", nl:"Kwart over vier.", en:"Quarter past four." },
  { id:103, cat:"Time & Dates", nl:"Half vijf.", en:"Half past four (lit. 'half five')." },
  { id:104, cat:"Time & Dates", nl:"Kwart voor zes.", en:"Quarter to six." },
  { id:105, cat:"Time & Dates", nl:"Vandaag is het maandag.", en:"Today is Monday." },
  { id:106, cat:"Time & Dates", nl:"Morgen is het dinsdag.", en:"Tomorrow is Tuesday." },
  { id:107, cat:"Time & Dates", nl:"Gisteren was het zondag.", en:"Yesterday was Sunday." },
  { id:108, cat:"Time & Dates", nl:"Deze week.", en:"This week." },
  { id:109, cat:"Time & Dates", nl:"Volgende week.", en:"Next week." },
  { id:110, cat:"Time & Dates", nl:"Vorige week.", en:"Last week." },
  { id:111, cat:"Time & Dates", nl:"Welke datum is het vandaag?", en:"What date is it today?" },
  { id:112, cat:"Time & Dates", nl:"Het is de vijfde januari.", en:"It is the fifth of January." },
  { id:113, cat:"Time & Dates", nl:"Hoe laat vertrekt de trein?", en:"What time does the train depart?" },
  { id:114, cat:"Time & Dates", nl:"Om halftien.", en:"At half past nine." },
  { id:115, cat:"Time & Dates", nl:"Ik heb een afspraak om twee uur.", en:"I have an appointment at two o'clock." },
  { id:116, cat:"Time & Dates", nl:"Het duurt ongeveer een uur.", en:"It takes about an hour." },
  { id:117, cat:"Time & Dates", nl:"Wacht even!", en:"Wait a moment!" },
  { id:118, cat:"Time & Dates", nl:"Zo snel mogelijk.", en:"As quickly as possible." },
  { id:119, cat:"Time & Dates", nl:"Over vijf minuten.", en:"In five minutes." },
  { id:120, cat:"Time & Dates", nl:"Te laat!", en:"Too late!" },

  // ===== SUPERMARKET & SHOPPING (121–160) =====
  { id:121, cat:"Supermarket & Shopping", nl:"Waar kan ik [product] vinden?", en:"Where can I find [product]?" },
  { id:122, cat:"Supermarket & Shopping", nl:"Ik zoek de afdeling zuivel.", en:"I'm looking for the dairy section." },
  { id:123, cat:"Supermarket & Shopping", nl:"Heeft u biologische groenten?", en:"Do you have organic vegetables?" },
  { id:124, cat:"Supermarket & Shopping", nl:"Hoeveel kost een kilo appels?", en:"How much does a kilo of apples cost?" },
  { id:125, cat:"Supermarket & Shopping", nl:"Ik wil graag twee liter melk.", en:"I would like two litres of milk." },
  { id:126, cat:"Supermarket & Shopping", nl:"Kunt u dit snijden?", en:"Can you slice this?" },
  { id:127, cat:"Supermarket & Shopping", nl:"Is dit vers?", en:"Is this fresh?" },
  { id:128, cat:"Supermarket & Shopping", nl:"Wat is de houdbaarheidsdatum?", en:"What is the expiry date?" },
  { id:129, cat:"Supermarket & Shopping", nl:"Ik heb een boodschappenlijstje.", en:"I have a shopping list." },
  { id:130, cat:"Supermarket & Shopping", nl:"Ik betaal met pinpas.", en:"I'll pay by debit card." },
  { id:131, cat:"Supermarket & Shopping", nl:"Ik betaal contant.", en:"I'll pay cash." },
  { id:132, cat:"Supermarket & Shopping", nl:"Heeft u een bonuskaart?", en:"Do you have a loyalty card?" },
  { id:133, cat:"Supermarket & Shopping", nl:"Mag ik een tasje?", en:"Can I have a bag?" },
  { id:134, cat:"Supermarket & Shopping", nl:"Heeft u statiegeld flessen?", en:"Do you have deposit bottles?" },
  { id:135, cat:"Supermarket & Shopping", nl:"Waar is de kassa?", en:"Where is the checkout?" },
  { id:136, cat:"Supermarket & Shopping", nl:"Kan ik hier pinnen?", en:"Can I pay by card here?" },
  { id:137, cat:"Supermarket & Shopping", nl:"Dit is op aanbieding.", en:"This is on offer / on sale." },
  { id:138, cat:"Supermarket & Shopping", nl:"Ik wil dit retourneren.", en:"I would like to return this." },
  { id:139, cat:"Supermarket & Shopping", nl:"Heeft u een bon voor mij?", en:"Can I have a receipt?" },
  { id:140, cat:"Supermarket & Shopping", nl:"Waar is de zelfbediening?", en:"Where is the self-checkout?" },
  { id:141, cat:"Supermarket & Shopping", nl:"Ik zoek een jas in maat medium.", en:"I'm looking for a jacket in size medium." },
  { id:142, cat:"Supermarket & Shopping", nl:"Mag ik dit passen?", en:"May I try this on?" },
  { id:143, cat:"Supermarket & Shopping", nl:"Waar zijn de paskamers?", en:"Where are the fitting rooms?" },
  { id:144, cat:"Supermarket & Shopping", nl:"Dit is te groot.", en:"This is too big." },
  { id:145, cat:"Supermarket & Shopping", nl:"Dit is te klein.", en:"This is too small." },
  { id:146, cat:"Supermarket & Shopping", nl:"Doet u het voor [bedrag]?", en:"Will you do it for [amount]?" },
  { id:147, cat:"Supermarket & Shopping", nl:"Is er korting op?", en:"Is there a discount on it?" },
  { id:148, cat:"Supermarket & Shopping", nl:"Ik kijk alleen maar.", en:"I'm just looking." },
  { id:149, cat:"Supermarket & Shopping", nl:"Ik neem dit.", en:"I'll take this." },
  { id:150, cat:"Supermarket & Shopping", nl:"Kunt u het inpakken als cadeau?", en:"Can you wrap it as a gift?" },
  { id:151, cat:"Supermarket & Shopping", nl:"Heeft u dit ook in het rood?", en:"Do you have this in red as well?" },
  { id:152, cat:"Supermarket & Shopping", nl:"Waar staan de snoepjes?", en:"Where is the candy / sweets?" },
  { id:153, cat:"Supermarket & Shopping", nl:"Ik zoek de drogisterij.", en:"I'm looking for the drugstore." },
  { id:154, cat:"Supermarket & Shopping", nl:"Ik heb brood nodig.", en:"I need bread." },
  { id:155, cat:"Supermarket & Shopping", nl:"Zijn er acties deze week?", en:"Are there any deals this week?" },
  { id:156, cat:"Supermarket & Shopping", nl:"Kan ik terugkomen voor een ruil?", en:"Can I come back for an exchange?" },
  { id:157, cat:"Supermarket & Shopping", nl:"Dit is beschadigd.", en:"This is damaged." },
  { id:158, cat:"Supermarket & Shopping", nl:"Ik zoek de bakkerij.", en:"I'm looking for the bakery." },
  { id:159, cat:"Supermarket & Shopping", nl:"Hoeveel mag ik er meenemen?", en:"How many may I take?" },
  { id:160, cat:"Supermarket & Shopping", nl:"Geeft u mij een kilo aardappelen.", en:"Give me a kilo of potatoes." },

  // ===== FOOD & RESTAURANTS (161–195) =====
  { id:161, cat:"Food & Restaurants", nl:"Een tafel voor twee, alsjeblieft.", en:"A table for two, please." },
  { id:162, cat:"Food & Restaurants", nl:"Heeft u een reservering?", en:"Do you have a reservation?" },
  { id:163, cat:"Food & Restaurants", nl:"Ik heb een reservering op naam van...", en:"I have a reservation under the name of..." },
  { id:164, cat:"Food & Restaurants", nl:"Mag ik de menukaart?", en:"May I have the menu?" },
  { id:165, cat:"Food & Restaurants", nl:"Wat is de dagschotel?", en:"What is today's special?" },
  { id:166, cat:"Food & Restaurants", nl:"Ik ben vegetariër.", en:"I am vegetarian." },
  { id:167, cat:"Food & Restaurants", nl:"Ik ben vegan.", en:"I am vegan." },
  { id:168, cat:"Food & Restaurants", nl:"Ik ben allergisch voor noten.", en:"I am allergic to nuts." },
  { id:169, cat:"Food & Restaurants", nl:"Bevat dit gluten?", en:"Does this contain gluten?" },
  { id:170, cat:"Food & Restaurants", nl:"Ik wil graag de kip, alsjeblieft.", en:"I would like the chicken, please." },
  { id:171, cat:"Food & Restaurants", nl:"Mag ik iets te drinken bestellen?", en:"May I order something to drink?" },
  { id:172, cat:"Food & Restaurants", nl:"Een glas water, alsjeblieft.", en:"A glass of water, please." },
  { id:173, cat:"Food & Restaurants", nl:"Een kopje koffie, graag.", en:"A cup of coffee, please." },
  { id:174, cat:"Food & Restaurants", nl:"Mag ik de rekening, alsjeblieft?", en:"May I have the bill, please?" },
  { id:175, cat:"Food & Restaurants", nl:"We splitsen de rekening.", en:"We'll split the bill." },
  { id:176, cat:"Food & Restaurants", nl:"Het was heerlijk!", en:"It was delicious!" },
  { id:177, cat:"Food & Restaurants", nl:"Het smaakt goed.", en:"It tastes good." },
  { id:178, cat:"Food & Restaurants", nl:"Iets meer peper, alsjeblieft.", en:"A little more pepper, please." },
  { id:179, cat:"Food & Restaurants", nl:"Mag ik een servetje?", en:"May I have a napkin?" },
  { id:180, cat:"Food & Restaurants", nl:"Ik heb honger.", en:"I am hungry." },
  { id:181, cat:"Food & Restaurants", nl:"Ik heb dorst.", en:"I am thirsty." },
  { id:182, cat:"Food & Restaurants", nl:"Ik wil graag een broodje.", en:"I would like a sandwich." },
  { id:183, cat:"Food & Restaurants", nl:"Doe maar een kroket.", en:"I'll have a croquette." },
  { id:184, cat:"Food & Restaurants", nl:"Een patatje met, alsjeblieft.", en:"Chips with mayo, please." },
  { id:185, cat:"Food & Restaurants", nl:"Nog een biertje, alsjeblieft.", en:"Another beer, please." },
  { id:186, cat:"Food & Restaurants", nl:"Heeft u oat milk?", en:"Do you have oat milk?" },
  { id:187, cat:"Food & Restaurants", nl:"Gaat u al weg?", en:"Are you leaving already?" },
  { id:188, cat:"Food & Restaurants", nl:"Het was te zout.", en:"It was too salty." },
  { id:189, cat:"Food & Restaurants", nl:"Mag ik iets anders bestellen?", en:"May I order something else?" },
  { id:190, cat:"Food & Restaurants", nl:"Kunt u het meenemen verpakken?", en:"Can you pack it to take away?" },
  { id:191, cat:"Food & Restaurants", nl:"Ik neem het mee.", en:"I'll take it to go." },
  { id:192, cat:"Food & Restaurants", nl:"Een stroopwafel bij de koffie?", en:"A stroopwafel with the coffee?" },
  { id:193, cat:"Food & Restaurants", nl:"Wat zit er in dit gerecht?", en:"What is in this dish?" },
  { id:194, cat:"Food & Restaurants", nl:"Is het pittig?", en:"Is it spicy?" },
  { id:195, cat:"Food & Restaurants", nl:"Dat is erg lekker!", en:"That is very tasty!" },

  // ===== TRANSPORT (196–225) =====
  { id:196, cat:"Transport", nl:"Waar kan ik een OV-chipkaart kopen?", en:"Where can I buy an OV-chipkaart?" },
  { id:197, cat:"Transport", nl:"Ik wil mijn OV-chipkaart opladen.", en:"I want to top up my OV-chipkaart." },
  { id:198, cat:"Transport", nl:"Vergeet niet in te checken!", en:"Don't forget to check in!" },
  { id:199, cat:"Transport", nl:"Welke lijn gaat naar het centrum?", en:"Which line goes to the city centre?" },
  { id:200, cat:"Transport", nl:"Hoe laat vertrekt de volgende tram?", en:"What time does the next tram depart?" },
  { id:201, cat:"Transport", nl:"Ik wil naar Centraal Station.", en:"I want to go to Central Station." },
  { id:202, cat:"Transport", nl:"Een enkeltje naar Utrecht, alsjeblieft.", en:"A single ticket to Utrecht, please." },
  { id:203, cat:"Transport", nl:"Een retourtje naar Den Haag.", en:"A return ticket to The Hague." },
  { id:204, cat:"Transport", nl:"Moet ik overstappen?", en:"Do I need to change trains?" },
  { id:205, cat:"Transport", nl:"De trein heeft vertraging.", en:"The train is delayed." },
  { id:206, cat:"Transport", nl:"Op welk spoor staat de trein?", en:"On which platform is the train?" },
  { id:207, cat:"Transport", nl:"Is deze stoel vrij?", en:"Is this seat free?" },
  { id:208, cat:"Transport", nl:"Mag ik hier zitten?", en:"May I sit here?" },
  { id:209, cat:"Transport", nl:"Ik wil een fiets huren.", en:"I want to hire a bicycle." },
  { id:210, cat:"Transport", nl:"Waar kan ik een OV-fiets huren?", en:"Where can I hire an OV-bike?" },
  { id:211, cat:"Transport", nl:"Mijn band is lek.", en:"My tyre is flat." },
  { id:212, cat:"Transport", nl:"Heeft u een fietspomp?", en:"Do you have a bicycle pump?" },
  { id:213, cat:"Transport", nl:"Het fietspad is aan de rechterkant.", en:"The cycle path is on the right." },
  { id:214, cat:"Transport", nl:"Ik zoek een parkeerplek.", en:"I'm looking for a parking space." },
  { id:215, cat:"Transport", nl:"Hoeveel kost het parkeren?", en:"How much does parking cost?" },
  { id:216, cat:"Transport", nl:"Kunt u een taxi bellen?", en:"Can you call a taxi?" },
  { id:217, cat:"Transport", nl:"Ik heb een Uber besteld.", en:"I have ordered an Uber." },
  { id:218, cat:"Transport", nl:"Hoe lang duurt de rit?", en:"How long does the journey take?" },
  { id:219, cat:"Transport", nl:"Stop hier maar, alsjeblieft.", en:"Stop here, please." },
  { id:220, cat:"Transport", nl:"De metro gaat om middernacht dicht.", en:"The metro closes at midnight." },
  { id:221, cat:"Transport", nl:"Ik wil naar het vliegveld Schiphol.", en:"I want to go to Schiphol airport." },
  { id:222, cat:"Transport", nl:"Is de bus op tijd?", en:"Is the bus on time?" },
  { id:223, cat:"Transport", nl:"Sluit de deur, alsjeblieft.", en:"Please close the door." },
  { id:224, cat:"Transport", nl:"Mag ik er hier uit?", en:"May I get off here?" },
  { id:225, cat:"Transport", nl:"Ik heb me vergist van trein.", en:"I got on the wrong train." },

  // ===== DIRECTIONS (226–245) =====
  { id:226, cat:"Directions", nl:"Kunt u mij de weg wijzen?", en:"Can you show me the way?" },
  { id:227, cat:"Directions", nl:"Ga rechtdoor.", en:"Go straight ahead." },
  { id:228, cat:"Directions", nl:"Sla linksaf.", en:"Turn left." },
  { id:229, cat:"Directions", nl:"Sla rechtsaf.", en:"Turn right." },
  { id:230, cat:"Directions", nl:"Aan het einde van de straat.", en:"At the end of the street." },
  { id:231, cat:"Directions", nl:"Over de brug.", en:"Over the bridge." },
  { id:232, cat:"Directions", nl:"Naast de bakkerij.", en:"Next to the bakery." },
  { id:233, cat:"Directions", nl:"Het is op loopafstand.", en:"It is within walking distance." },
  { id:234, cat:"Directions", nl:"Ongeveer 500 meter verder.", en:"Approximately 500 metres further." },
  { id:235, cat:"Directions", nl:"U kunt het niet missen.", en:"You can't miss it." },
  { id:236, cat:"Directions", nl:"Tegenover het station.", en:"Opposite the station." },
  { id:237, cat:"Directions", nl:"Op de hoek van de straat.", en:"On the corner of the street." },
  { id:238, cat:"Directions", nl:"Na de stoplichten.", en:"After the traffic lights." },
  { id:239, cat:"Directions", nl:"Ik ben de weg kwijt.", en:"I am lost." },
  { id:240, cat:"Directions", nl:"Kunt u dat op de kaart aanwijzen?", en:"Can you point it out on the map?" },
  { id:241, cat:"Directions", nl:"Hoe ver is het lopen?", en:"How far is it to walk?" },
  { id:242, cat:"Directions", nl:"Volg de borden.", en:"Follow the signs." },
  { id:243, cat:"Directions", nl:"Het is in het centrum.", en:"It is in the city centre." },
  { id:244, cat:"Directions", nl:"Ga de trap op.", en:"Go up the stairs." },
  { id:245, cat:"Directions", nl:"Het is op de eerste verdieping.", en:"It is on the first floor." },

  // ===== AT HOME (246–270) =====
  { id:246, cat:"At Home", nl:"Ik zoek een huurwoning.", en:"I am looking for a rental property." },
  { id:247, cat:"At Home", nl:"Hoeveel is de huur per maand?", en:"How much is the rent per month?" },
  { id:248, cat:"At Home", nl:"Is de borg inbegrepen?", en:"Is the deposit included?" },
  { id:249, cat:"At Home", nl:"De verwarming doet het niet.", en:"The heating is not working." },
  { id:250, cat:"At Home", nl:"Er is een lekkage.", en:"There is a leak." },
  { id:251, cat:"At Home", nl:"Wanneer komt de monteur?", en:"When is the repair person coming?" },
  { id:252, cat:"At Home", nl:"Ik wil de huur opzeggen.", en:"I want to terminate the rental agreement." },
  { id:253, cat:"At Home", nl:"Wij hebben nieuwe buren.", en:"We have new neighbours." },
  { id:254, cat:"At Home", nl:"Het is te luidruchtig bij de buren.", en:"It is too noisy at the neighbours'." },
  { id:255, cat:"At Home", nl:"Ik doe de was.", en:"I am doing the laundry." },
  { id:256, cat:"At Home", nl:"Waar is de wasmachine?", en:"Where is the washing machine?" },
  { id:257, cat:"At Home", nl:"Mag ik de vuilnis hier neerzetten?", en:"Can I put the rubbish here?" },
  { id:258, cat:"At Home", nl:"Welke kleur mag de vuilniszak zijn?", en:"What colour should the rubbish bag be?" },
  { id:259, cat:"At Home", nl:"Ik ga stofzuigen.", en:"I am going to vacuum." },
  { id:260, cat:"At Home", nl:"Zet de koffie maar aan.", en:"Go ahead and put the coffee on." },
  { id:261, cat:"At Home", nl:"Doe de deur op slot.", en:"Lock the door." },
  { id:262, cat:"At Home", nl:"Ik ben mijn sleutels kwijt.", en:"I have lost my keys." },
  { id:263, cat:"At Home", nl:"Mag ik thuis werken?", en:"May I work from home?" },
  { id:264, cat:"At Home", nl:"Het wifi-wachtwoord is...", en:"The wifi password is..." },
  { id:265, cat:"At Home", nl:"De stroom is uitgevallen.", en:"The power has gone out." },
  { id:266, cat:"At Home", nl:"Ik bel de verhuurder.", en:"I will call the landlord." },
  { id:267, cat:"At Home", nl:"Kunnen we de afval scheiden?", en:"Can we separate the waste?" },
  { id:268, cat:"At Home", nl:"Het is koud in huis.", en:"It is cold in the house." },
  { id:269, cat:"At Home", nl:"Zet de thermostaat hoger.", en:"Turn the thermostat up." },
  { id:270, cat:"At Home", nl:"Ik heb een pakketje ontvangen.", en:"I have received a parcel." },

  // ===== WORK & STUDY (271–295) =====
  { id:271, cat:"Work & Study", nl:"Ik begin om negen uur.", en:"I start at nine o'clock." },
  { id:272, cat:"Work & Study", nl:"Ik heb een vergadering.", en:"I have a meeting." },
  { id:273, cat:"Work & Study", nl:"Kunt u mij doorverbinden?", en:"Can you put me through?" },
  { id:274, cat:"Work & Study", nl:"Ik bel terug.", en:"I will call back." },
  { id:275, cat:"Work & Study", nl:"Kunt u een e-mail sturen?", en:"Can you send an email?" },
  { id:276, cat:"Work & Study", nl:"De deadline is vrijdag.", en:"The deadline is Friday." },
  { id:277, cat:"Work & Study", nl:"Ik werk op afstand.", en:"I work remotely." },
  { id:278, cat:"Work & Study", nl:"Ik ben ziek vandaag.", en:"I am ill today." },
  { id:279, cat:"Work & Study", nl:"Ik neem vrij morgen.", en:"I am taking tomorrow off." },
  { id:280, cat:"Work & Study", nl:"Mijn contract loopt af.", en:"My contract is expiring." },
  { id:281, cat:"Work & Study", nl:"Ik wil vakantiedagen opnemen.", en:"I want to take holiday days." },
  { id:282, cat:"Work & Study", nl:"Kan ik het rapport later insturen?", en:"Can I send the report later?" },
  { id:283, cat:"Work & Study", nl:"De printer doet het niet.", en:"The printer is not working." },
  { id:284, cat:"Work & Study", nl:"Ik heb een nieuwe collega.", en:"I have a new colleague." },
  { id:285, cat:"Work & Study", nl:"We gaan lunchen.", en:"We are going for lunch." },
  { id:286, cat:"Work & Study", nl:"Ik schrijf me in voor een cursus.", en:"I am enrolling in a course." },
  { id:287, cat:"Work & Study", nl:"Ik zoek een stage.", en:"I am looking for an internship." },
  { id:288, cat:"Work & Study", nl:"Ik ben ingeschreven bij de gemeente.", en:"I am registered with the municipality." },
  { id:289, cat:"Work & Study", nl:"Ik moet DigiD aanvragen.", en:"I need to apply for DigiD." },
  { id:290, cat:"Work & Study", nl:"Kunt u dit document ondertekenen?", en:"Can you sign this document?" },
  { id:291, cat:"Work & Study", nl:"Ik heb mijn BSN nodig.", en:"I need my BSN (citizen service number)." },
  { id:292, cat:"Work & Study", nl:"Wanneer is de loonstrook beschikbaar?", en:"When is the pay slip available?" },
  { id:293, cat:"Work & Study", nl:"Ik volg een taalcursus.", en:"I am taking a language course." },
  { id:294, cat:"Work & Study", nl:"Mijn stageplek is in Rotterdam.", en:"My internship is in Rotterdam." },
  { id:295, cat:"Work & Study", nl:"We houden een teamuitje.", en:"We are having a team outing." },

  // ===== HEALTH & PHARMACY (296–320) =====
  { id:296, cat:"Health & Pharmacy", nl:"Ik voel me niet goed.", en:"I don't feel well." },
  { id:297, cat:"Health & Pharmacy", nl:"Ik heb pijn in mijn buik.", en:"I have stomach pain." },
  { id:298, cat:"Health & Pharmacy", nl:"Ik heb hoofdpijn.", en:"I have a headache." },
  { id:299, cat:"Health & Pharmacy", nl:"Ik heb koorts.", en:"I have a fever." },
  { id:300, cat:"Health & Pharmacy", nl:"Ik heb me bezeerd.", en:"I have hurt myself." },
  { id:301, cat:"Health & Pharmacy", nl:"Ik moet naar de dokter.", en:"I need to go to the doctor." },
  { id:302, cat:"Health & Pharmacy", nl:"Ik wil een afspraak maken.", en:"I want to make an appointment." },
  { id:303, cat:"Health & Pharmacy", nl:"Ik ben ingeschreven bij de huisarts.", en:"I am registered with the GP." },
  { id:304, cat:"Health & Pharmacy", nl:"Kunt u mij iets voorschrijven?", en:"Can you prescribe something for me?" },
  { id:305, cat:"Health & Pharmacy", nl:"Ik heb een recept nodig.", en:"I need a prescription." },
  { id:306, cat:"Health & Pharmacy", nl:"Heeft u paracetamol?", en:"Do you have paracetamol?" },
  { id:307, cat:"Health & Pharmacy", nl:"Hoe vaak moet ik dit innemen?", en:"How often should I take this?" },
  { id:308, cat:"Health & Pharmacy", nl:"Ik ben allergisch voor penicilline.", en:"I am allergic to penicillin." },
  { id:309, cat:"Health & Pharmacy", nl:"Kunt u dit medicijn bestellen?", en:"Can you order this medication?" },
  { id:310, cat:"Health & Pharmacy", nl:"Ik heb een zorgverzekering.", en:"I have health insurance." },
  { id:311, cat:"Health & Pharmacy", nl:"Wat is het eigen risico?", en:"What is the deductible (eigen risico)?" },
  { id:312, cat:"Health & Pharmacy", nl:"Ik bel de doktersdienst.", en:"I am calling the out-of-hours GP service." },
  { id:313, cat:"Health & Pharmacy", nl:"Is er een apotheek in de buurt?", en:"Is there a pharmacy nearby?" },
  { id:314, cat:"Health & Pharmacy", nl:"Het is dringend.", en:"It is urgent." },
  { id:315, cat:"Health & Pharmacy", nl:"Bel een ambulance!", en:"Call an ambulance!" },
  { id:316, cat:"Health & Pharmacy", nl:"Ik heb moeite met slapen.", en:"I have trouble sleeping." },
  { id:317, cat:"Health & Pharmacy", nl:"Ik heb last van stress.", en:"I am suffering from stress." },
  { id:318, cat:"Health & Pharmacy", nl:"Ik zoek een tandarts.", en:"I am looking for a dentist." },
  { id:319, cat:"Health & Pharmacy", nl:"Mijn tand doet pijn.", en:"My tooth hurts." },
  { id:320, cat:"Health & Pharmacy", nl:"Ik ben zwanger.", en:"I am pregnant." },

  // ===== WEATHER (321–340) =====
  { id:321, cat:"Weather", nl:"Wat is het weerbericht?", en:"What is the weather forecast?" },
  { id:322, cat:"Weather", nl:"Het is mooi weer vandaag.", en:"The weather is nice today." },
  { id:323, cat:"Weather", nl:"Het regent.", en:"It is raining." },
  { id:324, cat:"Weather", nl:"Neem een paraplu mee.", en:"Take an umbrella with you." },
  { id:325, cat:"Weather", nl:"Het is bewolkt.", en:"It is cloudy." },
  { id:326, cat:"Weather", nl:"Het vriest vannacht.", en:"It will freeze tonight." },
  { id:327, cat:"Weather", nl:"Het is ijskoud!", en:"It is freezing cold!" },
  { id:328, cat:"Weather", nl:"Het is lekker warm.", en:"It is pleasantly warm." },
  { id:329, cat:"Weather", nl:"Er staat veel wind.", en:"There is a lot of wind." },
  { id:330, cat:"Weather", nl:"Er is een storm op komst.", en:"There is a storm coming." },
  { id:331, cat:"Weather", nl:"Het sneeuwt!", en:"It is snowing!" },
  { id:332, cat:"Weather", nl:"Het wordt beter morgen.", en:"It will get better tomorrow." },
  { id:333, cat:"Weather", nl:"Typisch Hollands weer!", en:"Typical Dutch weather!" },
  { id:334, cat:"Weather", nl:"Kleed je warm aan.", en:"Dress warmly." },
  { id:335, cat:"Weather", nl:"Het is erg vochtig.", en:"It is very humid." },
  { id:336, cat:"Weather", nl:"De zon schijnt.", en:"The sun is shining." },
  { id:337, cat:"Weather", nl:"Er is mist.", en:"There is fog." },
  { id:338, cat:"Weather", nl:"Hoeveel graden is het?", en:"How many degrees is it?" },
  { id:339, cat:"Weather", nl:"Het is tien graden buiten.", en:"It is ten degrees outside." },
  { id:340, cat:"Weather", nl:"Fijn dat het zomer is!", en:"Great that it's summer!" },

  // ===== SOCIAL SITUATIONS (341–370) =====
  { id:341, cat:"Social Situations", nl:"Zullen we iets drinken?", en:"Shall we get a drink?" },
  { id:342, cat:"Social Situations", nl:"Ik trakteer!", en:"It's my treat!" },
  { id:343, cat:"Social Situations", nl:"We doen ieder voor zich.", en:"We'll go Dutch (each pays for themselves)." },
  { id:344, cat:"Social Situations", nl:"Ga je mee naar het feest?", en:"Are you coming to the party?" },
  { id:345, cat:"Social Situations", nl:"Leuk!", en:"Fun! / Nice!" },
  { id:346, cat:"Social Situations", nl:"Wat jammer!", en:"What a pity!" },
  { id:347, cat:"Social Situations", nl:"Ik kan helaas niet.", en:"Unfortunately I cannot." },
  { id:348, cat:"Social Situations", nl:"Een andere keer misschien?", en:"Another time maybe?" },
  { id:349, cat:"Social Situations", nl:"Hoe laat beginnen we?", en:"What time do we start?" },
  { id:350, cat:"Social Situations", nl:"Ik kom om acht uur.", en:"I'll come at eight o'clock." },
  { id:351, cat:"Social Situations", nl:"Ik ben een beetje te laat.", en:"I am a little late." },
  { id:352, cat:"Social Situations", nl:"Ik ben er bijna!", en:"I'm almost there!" },
  { id:353, cat:"Social Situations", nl:"Wat doe jij dit weekend?", en:"What are you doing this weekend?" },
  { id:354, cat:"Social Situations", nl:"Ik ga naar de markt.", en:"I am going to the market." },
  { id:355, cat:"Social Situations", nl:"We gaan een dagje Keukenhof.", en:"We're going to Keukenhof for the day." },
  { id:356, cat:"Social Situations", nl:"Heb je kinderen?", en:"Do you have children?" },
  { id:357, cat:"Social Situations", nl:"Houd je van voetbal?", en:"Do you like football?" },
  { id:358, cat:"Social Situations", nl:"Ik ben fan van Ajax.", en:"I am a fan of Ajax." },
  { id:359, cat:"Social Situations", nl:"Direct zijn is normaal hier.", en:"Being direct is normal here." },
  { id:360, cat:"Social Situations", nl:"Doe maar gewoon, dan doe je al gek genoeg.", en:"Just act normal, that's crazy enough." },
  { id:361, cat:"Social Situations", nl:"Mag ik jou iets vragen?", en:"May I ask you something?" },
  { id:362, cat:"Social Situations", nl:"Wil je meer weten?", en:"Do you want to know more?" },
  { id:363, cat:"Social Situations", nl:"Dat vind ik ook!", en:"I think so too!" },
  { id:364, cat:"Social Situations", nl:"Ik ben het daar niet mee eens.", en:"I don't agree with that." },
  { id:365, cat:"Social Situations", nl:"Wat vind jij?", en:"What do you think?" },
  { id:366, cat:"Social Situations", nl:"Hoe is je dag geweest?", en:"How was your day?" },
  { id:367, cat:"Social Situations", nl:"Druk gehad!", en:"Been busy!" },
  { id:368, cat:"Social Situations", nl:"Heb je al gegeten?", en:"Have you eaten yet?" },
  { id:369, cat:"Social Situations", nl:"Zullen we naar de bios gaan?", en:"Shall we go to the cinema?" },
  { id:370, cat:"Social Situations", nl:"Gezellig!", en:"Cosy / Nice vibes! (untranslatable Dutch concept)" },

  // ===== BANKING & ADMIN (371–390) =====
  { id:371, cat:"Banking & Admin", nl:"Ik wil een rekening openen.", en:"I want to open an account." },
  { id:372, cat:"Banking & Admin", nl:"Wat is uw IBAN?", en:"What is your IBAN?" },
  { id:373, cat:"Banking & Admin", nl:"Ik wil geld overboeken.", en:"I want to transfer money." },
  { id:374, cat:"Banking & Admin", nl:"Mijn bankpas werkt niet.", en:"My bank card is not working." },
  { id:375, cat:"Banking & Admin", nl:"Kan ik de pincode wijzigen?", en:"Can I change the PIN?" },
  { id:376, cat:"Banking & Admin", nl:"Ik ben mijn bankpas verloren.", en:"I have lost my bank card." },
  { id:377, cat:"Banking & Admin", nl:"Ik wil mijn kaart blokkeren.", en:"I want to block my card." },
  { id:378, cat:"Banking & Admin", nl:"Hoeveel staat er op mijn rekening?", en:"How much is in my account?" },
  { id:379, cat:"Banking & Admin", nl:"Ik heb een DigiD nodig.", en:"I need a DigiD." },
  { id:380, cat:"Banking & Admin", nl:"Ik moet me inschrijven bij de gemeente.", en:"I need to register with the municipality." },
  { id:381, cat:"Banking & Admin", nl:"Ik zoek een belastingadviseur.", en:"I am looking for a tax advisor." },
  { id:382, cat:"Banking & Admin", nl:"Wat is mijn BSN-nummer?", en:"What is my BSN number?" },
  { id:383, cat:"Banking & Admin", nl:"Ik moet aangifte doen.", en:"I need to file a tax return." },
  { id:384, cat:"Banking & Admin", nl:"Kunt u mij helpen met het formulier?", en:"Can you help me with the form?" },
  { id:385, cat:"Banking & Admin", nl:"Ik heb mijn paspoort nodig.", en:"I need my passport." },
  { id:386, cat:"Banking & Admin", nl:"Mijn verblijfsvergunning verloopt.", en:"My residence permit is expiring." },
  { id:387, cat:"Banking & Admin", nl:"Ik ontvang een toelage.", en:"I receive an allowance / benefit." },
  { id:388, cat:"Banking & Admin", nl:"Ik wil een verzekering afsluiten.", en:"I want to take out insurance." },
  { id:389, cat:"Banking & Admin", nl:"Wanneer is de belastingdienst open?", en:"When is the tax authority open?" },
  { id:390, cat:"Banking & Admin", nl:"Kunt u dit per post versturen?", en:"Can you send this by post?" },

  // ===== FEELINGS & EMOTIONS (391–410) =====
  { id:391, cat:"Feelings & Emotions", nl:"Ik ben blij.", en:"I am happy." },
  { id:392, cat:"Feelings & Emotions", nl:"Ik ben verdrietig.", en:"I am sad." },
  { id:393, cat:"Feelings & Emotions", nl:"Ik ben moe.", en:"I am tired." },
  { id:394, cat:"Feelings & Emotions", nl:"Ik ben nerveus.", en:"I am nervous." },
  { id:395, cat:"Feelings & Emotions", nl:"Ik ben gestrest.", en:"I am stressed." },
  { id:396, cat:"Feelings & Emotions", nl:"Ik ben opgewonden.", en:"I am excited." },
  { id:397, cat:"Feelings & Emotions", nl:"Ik voel me goed.", en:"I feel good." },
  { id:398, cat:"Feelings & Emotions", nl:"Ik voel me prima.", en:"I feel fine." },
  { id:399, cat:"Feelings & Emotions", nl:"Ik voel me niet lekker.", en:"I don't feel well." },
  { id:400, cat:"Feelings & Emotions", nl:"Ik mis mijn familie.", en:"I miss my family." },
  { id:401, cat:"Feelings & Emotions", nl:"Ik ben trots op mezelf.", en:"I am proud of myself." },
  { id:402, cat:"Feelings & Emotions", nl:"Het gaat beter.", en:"It is getting better." },
  { id:403, cat:"Feelings & Emotions", nl:"Ik maak me zorgen.", en:"I am worried." },
  { id:404, cat:"Feelings & Emotions", nl:"Dat vind ik jammer.", en:"I find that a pity." },
  { id:405, cat:"Feelings & Emotions", nl:"Dat maakt me boos.", en:"That makes me angry." },
  { id:406, cat:"Feelings & Emotions", nl:"Ik ben bang.", en:"I am afraid." },
  { id:407, cat:"Feelings & Emotions", nl:"Ik voel me eenzaam.", en:"I feel lonely." },
  { id:408, cat:"Feelings & Emotions", nl:"Ik ben verliefd.", en:"I am in love." },
  { id:409, cat:"Feelings & Emotions", nl:"Ik hou van je.", en:"I love you." },
  { id:410, cat:"Feelings & Emotions", nl:"Ik waardeer dat erg.", en:"I really appreciate that." },

  // ===== PHONE & INTERNET (411–425) =====
  { id:411, cat:"Phone & Internet", nl:"Spreek ik met [naam]?", en:"Am I speaking with [name]?" },
  { id:412, cat:"Phone & Internet", nl:"Met wie spreek ik?", en:"Who am I speaking with?" },
  { id:413, cat:"Phone & Internet", nl:"Ik bel om... te bespreken.", en:"I'm calling to discuss..." },
  { id:414, cat:"Phone & Internet", nl:"Kunt u terugbellen?", en:"Can you call back?" },
  { id:415, cat:"Phone & Internet", nl:"Ik hoor u niet goed.", en:"I can't hear you well." },
  { id:416, cat:"Phone & Internet", nl:"De lijn is slecht.", en:"The line is bad." },
  { id:417, cat:"Phone & Internet", nl:"Kunt u luider spreken?", en:"Can you speak louder?" },
  { id:418, cat:"Phone & Internet", nl:"Ik stuur een appje.", en:"I'll send a WhatsApp." },
  { id:419, cat:"Phone & Internet", nl:"Mijn telefoon is bijna leeg.", en:"My phone is almost dead." },
  { id:420, cat:"Phone & Internet", nl:"Heeft u een oplader?", en:"Do you have a charger?" },
  { id:421, cat:"Phone & Internet", nl:"Het wifi werkt niet.", en:"The wifi is not working." },
  { id:422, cat:"Phone & Internet", nl:"Kunt u het wachtwoord geven?", en:"Can you give me the password?" },
  { id:423, cat:"Phone & Internet", nl:"Ik heb een nieuwe sim nodig.", en:"I need a new SIM card." },
  { id:424, cat:"Phone & Internet", nl:"Mijn abonnement loopt af.", en:"My subscription is expiring." },
  { id:425, cat:"Phone & Internet", nl:"Ik heb geen bereik hier.", en:"I have no signal here." },

  // ===== EMERGENCIES (426–440) =====
  { id:426, cat:"Emergencies", nl:"Help!", en:"Help!" },
  { id:427, cat:"Emergencies", nl:"Bel de politie!", en:"Call the police!" },
  { id:428, cat:"Emergencies", nl:"Er is brand!", en:"There is a fire!" },
  { id:429, cat:"Emergencies", nl:"Bel een ambulance!", en:"Call an ambulance!" },
  { id:430, cat:"Emergencies", nl:"Ik ben bestolen.", en:"I have been robbed." },
  { id:431, cat:"Emergencies", nl:"Mijn portemonnee is gestolen.", en:"My wallet has been stolen." },
  { id:432, cat:"Emergencies", nl:"Ik ben gewond.", en:"I am injured." },
  { id:433, cat:"Emergencies", nl:"Er is een ongeluk gebeurd.", en:"An accident has happened." },
  { id:434, cat:"Emergencies", nl:"Ik heb een arts nodig.", en:"I need a doctor." },
  { id:435, cat:"Emergencies", nl:"Ik kan niet ademhalen.", en:"I cannot breathe." },
  { id:436, cat:"Emergencies", nl:"Verlies is gemeld bij de politie.", en:"The loss has been reported to the police." },
  { id:437, cat:"Emergencies", nl:"Laat me met rust!", en:"Leave me alone!" },
  { id:438, cat:"Emergencies", nl:"Hier is mijn paspoort.", en:"Here is my passport." },
  { id:439, cat:"Emergencies", nl:"Ik heb een tolk nodig.", en:"I need an interpreter." },
  { id:440, cat:"Emergencies", nl:"Het alarmnummer is 112.", en:"The emergency number is 112." },

  // ===== COMMON EXPRESSIONS & IDIOMS (441–475) =====
  { id:441, cat:"Expressions & Idioms", nl:"Doe normaal!", en:"Act normal! (common Dutch phrase)" },
  { id:442, cat:"Expressions & Idioms", nl:"Dat is niet normaal.", en:"That is not normal / That's crazy." },
  { id:443, cat:"Expressions & Idioms", nl:"Lekker bezig!", en:"Good job! / Nice one!" },
  { id:444, cat:"Expressions & Idioms", nl:"Toch?", en:"Right? / Isn't it?" },
  { id:445, cat:"Expressions & Idioms", nl:"Hè?", en:"Huh? / Right? (filler)" },
  { id:446, cat:"Expressions & Idioms", nl:"Nou ja.", en:"Well... (resignation / filler)" },
  { id:447, cat:"Expressions & Idioms", nl:"Eigenlijk...", en:"Actually..." },
  { id:448, cat:"Expressions & Idioms", nl:"Zo is dat!", en:"That's how it is!" },
  { id:449, cat:"Expressions & Idioms", nl:"Weet je wat?", en:"You know what?" },
  { id:450, cat:"Expressions & Idioms", nl:"Nou, dat is interessant.", en:"Well, that is interesting." },
  { id:451, cat:"Expressions & Idioms", nl:"In ieder geval.", en:"In any case / Anyway." },
  { id:452, cat:"Expressions & Idioms", nl:"Dat klopt.", en:"That is correct." },
  { id:453, cat:"Expressions & Idioms", nl:"Logisch!", en:"Of course! / Makes sense!" },
  { id:454, cat:"Expressions & Idioms", nl:"Ik heb er geen zin in.", en:"I don't feel like it." },
  { id:455, cat:"Expressions & Idioms", nl:"Dat zit wel snor.", en:"That's all good / sorted." },
  { id:456, cat:"Expressions & Idioms", nl:"Laat maar.", en:"Never mind / Forget it." },
  { id:457, cat:"Expressions & Idioms", nl:"Dat scheelt.", en:"That makes a difference." },
  { id:458, cat:"Expressions & Idioms", nl:"Druk druk druk.", en:"Busy busy busy." },
  { id:459, cat:"Expressions & Idioms", nl:"Zo te zien.", en:"It seems like / Apparently." },
  { id:460, cat:"Expressions & Idioms", nl:"Het valt mee.", en:"It's not that bad / Better than expected." },
  { id:461, cat:"Expressions & Idioms", nl:"Het valt tegen.", en:"It's disappointing / worse than expected." },
  { id:462, cat:"Expressions & Idioms", nl:"Ik maak het goed.", en:"I'll make it up to you." },
  { id:463, cat:"Expressions & Idioms", nl:"Dat is echt heel erg!", en:"That is really terrible!" },
  { id:464, cat:"Expressions & Idioms", nl:"Ik snap het.", en:"I get it / I understand." },
  { id:465, cat:"Expressions & Idioms", nl:"Zeg maar.", en:"Just say / You know." },
  { id:466, cat:"Expressions & Idioms", nl:"Hoe dan ook.", en:"Anyway / However." },
  { id:467, cat:"Expressions & Idioms", nl:"Helemaal niet.", en:"Not at all." },
  { id:468, cat:"Expressions & Idioms", nl:"Heel erg goed!", en:"Very well done!" },
  { id:469, cat:"Expressions & Idioms", nl:"Vet cool!", en:"Super cool!" },
  { id:470, cat:"Expressions & Idioms", nl:"Dat is gaaf!", en:"That is great / awesome!" },
  { id:471, cat:"Expressions & Idioms", nl:"Ik hoop het.", en:"I hope so." },
  { id:472, cat:"Expressions & Idioms", nl:"We zien wel.", en:"We'll see." },
  { id:473, cat:"Expressions & Idioms", nl:"Afgesproken!", en:"Agreed! / It's a deal!" },
  { id:474, cat:"Expressions & Idioms", nl:"Wat een toeval!", en:"What a coincidence!" },
  { id:475, cat:"Expressions & Idioms", nl:"Het is wat het is.", en:"It is what it is." },

  // ===== NEIGHBOURHOOD & DAILY LIFE (476–500) =====
  { id:476, cat:"Neighbourhood & Daily Life", nl:"Waar is de dichtstbijzijnde supermarkt?", en:"Where is the nearest supermarket?" },
  { id:477, cat:"Neighbourhood & Daily Life", nl:"Hoe laat gaat de bibliotheek open?", en:"What time does the library open?" },
  { id:478, cat:"Neighbourhood & Daily Life", nl:"Is er een sportschool in de buurt?", en:"Is there a gym nearby?" },
  { id:479, cat:"Neighbourhood & Daily Life", nl:"Waar kan ik de kinderopvang vinden?", en:"Where can I find childcare?" },
  { id:480, cat:"Neighbourhood & Daily Life", nl:"Is er een goed restaurant hier?", en:"Is there a good restaurant here?" },
  { id:481, cat:"Neighbourhood & Daily Life", nl:"Waar is het gemeentehuis?", en:"Where is the town hall?" },
  { id:482, cat:"Neighbourhood & Daily Life", nl:"Hoe laat gaat de prullenbak op?", en:"What time is rubbish collection?" },
  { id:483, cat:"Neighbourhood & Daily Life", nl:"Mag ik hier fietsen?", en:"Am I allowed to cycle here?" },
  { id:484, cat:"Neighbourhood & Daily Life", nl:"Waar kan ik mijn fiets stallen?", en:"Where can I park my bike?" },
  { id:485, cat:"Neighbourhood & Daily Life", nl:"De markt is op zaterdag.", en:"The market is on Saturday." },
  { id:486, cat:"Neighbourhood & Daily Life", nl:"Is er een speeltuin in de buurt?", en:"Is there a playground nearby?" },
  { id:487, cat:"Neighbourhood & Daily Life", nl:"Ik zoek een goede bakker.", en:"I'm looking for a good bakery." },
  { id:488, cat:"Neighbourhood & Daily Life", nl:"Heeft de Albert Heijn koopavond?", en:"Does the Albert Heijn have late opening?" },
  { id:489, cat:"Neighbourhood & Daily Life", nl:"Waar gooi ik glas in?", en:"Where do I put glass (recycling)?" },
  { id:490, cat:"Neighbourhood & Daily Life", nl:"Is het veilig hier 's avonds?", en:"Is it safe here in the evening?" },
  { id:491, cat:"Neighbourhood & Daily Life", nl:"Ik zoek de VVV voor toeristische informatie.", en:"I'm looking for the tourist information office." },
  { id:492, cat:"Neighbourhood & Daily Life", nl:"Wanneer is koningsdag?", en:"When is King's Day?" },
  { id:493, cat:"Neighbourhood & Daily Life", nl:"Ik wil me aansluiten bij een club.", en:"I want to join a club." },
  { id:494, cat:"Neighbourhood & Daily Life", nl:"De buren klagen over geluid.", en:"The neighbours are complaining about noise." },
  { id:495, cat:"Neighbourhood & Daily Life", nl:"Weet je een goed tandarts?", en:"Do you know a good dentist?" },
  { id:496, cat:"Neighbourhood & Daily Life", nl:"De trein rijdt niet vandaag.", en:"The train is not running today." },
  { id:497, cat:"Neighbourhood & Daily Life", nl:"Er is een evenement in het park.", en:"There is an event in the park." },
  { id:498, cat:"Neighbourhood & Daily Life", nl:"Ik ga een dagje de stad in.", en:"I'm going into the city for the day." },
  { id:499, cat:"Neighbourhood & Daily Life", nl:"Tot de volgende keer!", en:"Until next time!" },
  { id:500, cat:"Neighbourhood & Daily Life", nl:"Ik word elke dag beter in het Nederlands!", en:"I am getting better at Dutch every day!" },

  // ===== CYCLING LIFE (501–520) =====
  { id:501, cat:"Cycling Life", nl:"Pas op! Fietser!", en:"Watch out! Cyclist!" },
  { id:502, cat:"Cycling Life", nl:"Ik ga op de fiets.", en:"I'm going by bike." },
  { id:503, cat:"Cycling Life", nl:"Mijn fiets staat op slot.", en:"My bike is locked." },
  { id:504, cat:"Cycling Life", nl:"Ik heb mijn fiets niet op slot gezet.", en:"I didn't lock my bike." },
  { id:505, cat:"Cycling Life", nl:"Mijn fiets is gestolen!", en:"My bike has been stolen!" },
  { id:506, cat:"Cycling Life", nl:"Waar is de fietsenmaker?", en:"Where is the bike repair shop?" },
  { id:507, cat:"Cycling Life", nl:"Mijn ketting is eraf.", en:"My chain has come off." },
  { id:508, cat:"Cycling Life", nl:"Mijn rem doet het niet.", en:"My brake isn't working." },
  { id:509, cat:"Cycling Life", nl:"Ik zoek een fietsslot.", en:"I am looking for a bike lock." },
  { id:510, cat:"Cycling Life", nl:"Hoe lang duurt het op de fiets?", en:"How long does it take by bike?" },
  { id:511, cat:"Cycling Life", nl:"Het fietspad is alleen voor fietsers.", en:"The cycle path is for cyclists only." },
  { id:512, cat:"Cycling Life", nl:"Let op, de brug gaat omhoog.", en:"Watch out, the bridge is going up." },
  { id:513, cat:"Cycling Life", nl:"Mag ik mijn fiets hier neerzetten?", en:"Can I park my bike here?" },
  { id:514, cat:"Cycling Life", nl:"Ik heb lekke band.", en:"I have a flat tyre." },
  { id:515, cat:"Cycling Life", nl:"Ik heb een elektrische fiets.", en:"I have an electric bike." },
  { id:516, cat:"Cycling Life", nl:"Helm op!", en:"Helmet on!" },
  { id:517, cat:"Cycling Life", nl:"Geef een hand als je afslaat.", en:"Signal with your hand when turning." },
  { id:518, cat:"Cycling Life", nl:"Ik fietser er elke dag naartoe.", en:"I cycle there every day." },
  { id:519, cat:"Cycling Life", nl:"Kijk uit voor trams!", en:"Watch out for trams!" },
  { id:520, cat:"Cycling Life", nl:"Doe je licht aan — het is al donker.", en:"Turn your light on — it's already dark." },

  // ===== NUMBERS & QUANTITIES (521–530) =====
  { id:521, cat:"Numbers & Quantities", nl:"Hoeveel zijn het er?", en:"How many are there?" },
  { id:522, cat:"Numbers & Quantities", nl:"Geef me er twee, alsjeblieft.", en:"Give me two of them, please." },
  { id:523, cat:"Numbers & Quantities", nl:"Dat is te veel.", en:"That is too much." },
  { id:524, cat:"Numbers & Quantities", nl:"Dat is niet genoeg.", en:"That is not enough." },
  { id:525, cat:"Numbers & Quantities", nl:"Een beetje meer, alsjeblieft.", en:"A little more, please." },
  { id:526, cat:"Numbers & Quantities", nl:"De helft, alsjeblieft.", en:"Half of it, please." },
  { id:527, cat:"Numbers & Quantities", nl:"Dat kost vijfentwintig euro.", en:"That costs twenty-five euros." },
  { id:528, cat:"Numbers & Quantities", nl:"Heeft u gepast geld?", en:"Do you have exact change?" },
  { id:529, cat:"Numbers & Quantities", nl:"Ik heb geen kleingeld.", en:"I don't have any small change." },
  { id:530, cat:"Numbers & Quantities", nl:"Rond het af naar boven.", en:"Round it up." },
];

const cats = [...new Set(data.map(d => d.cat))];
const sel = document.getElementById('catFilter');
cats.forEach(c => {
  const o = document.createElement('option');
  o.value = c; o.textContent = c;
  sel.appendChild(o);
});

const catIcons = {
  "Greetings & Farewells":"👋","Introductions":"🙋","Basic Phrases":"💬","Questions":"❓","Time & Dates":"🕐","Supermarket & Shopping":"🛒","Food & Restaurants":"🍽️","Transport":"🚲","Directions":"🗺️","At Home":"🏠","Work & Study":"💼","Health & Pharmacy":"💊","Weather":"🌧️","Social Situations":"🎉","Banking & Admin":"🏦","Feelings & Emotions":"💛","Phone & Internet":"📱","Emergencies":"🚨","Expressions & Idioms":"🇳🇱","Neighbourhood & Daily Life":"🏙️","Cycling Life":"🚴","Numbers & Quantities":"🔢"
};

function filter() {
  const q = document.getElementById('search').value.toLowerCase();
  const cat = document.getElementById('catFilter').value;
  const filtered = data.filter(d =>
    (!cat || d.cat === cat) &&
    (!q || d.nl.toLowerCase().includes(q) || d.en.toLowerCase().includes(q))
  );
  render(filtered);
}

function render(items) {
  const main = document.getElementById('main');
  const byCat = {};
  items.forEach(d => {
    if (!byCat[d.cat]) byCat[d.cat] = [];
    byCat[d.cat].push(d);
  });
  const html = Object.entries(byCat).map(([cat, rows]) => `
    <div class="category-header">
      <span class="category-icon">${catIcons[cat]||'📌'}</span>${cat}
      <span class="cat-badge">${rows.length} sentences</span>
    </div>
    <div class="sentence-grid">
      ${rows.map(d => `
        <div class="card">
          <span class="num">#${d.id}</span>
          <div class="nl">${d.nl}</div>
          <div class="en">${d.en}</div>
        </div>`).join('')}
    </div>
  `).join('');
  main.innerHTML = html || `<div class="no-results">No sentences found. Try a different search.</div>`;
  document.getElementById('stats').textContent = `Showing ${items.length} of 530 sentences`;
}

render(data);
</script>
</body>
</html>
