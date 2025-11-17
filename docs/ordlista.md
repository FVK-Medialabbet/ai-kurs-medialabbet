# Ordlista – AI-begrepp för vardag och app-utveckling

> Den här ordlistan är framtagen november 2025 för Medialabbet/Katchapp.
> Fokus: begrepp inom AI kopplat till både vardagsanvändning och app-utveckling.

---

## 1. Grundläggande begrepp

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **AI (Artificiell intelligens)** | Datorer som gör saker som liknar mänsklig intelligens – t.ex. rekommendationer, stavningskontroll, röstassistenter. | Samlingsnamn för funktioner i din app som analyserar data, hjälper användare att fatta beslut eller skapar nytt innehåll (text, bild, ljud). |
| **ML (Machine Learning)** | Program som lär sig från data och blir bättre över tid, t.ex. spamfilter eller rekommendationer. | Modeller som tränas på historisk data (t.ex. närvarostatistik) för att förutsäga eller klassificera saker. |
| **Deep Learning / Djupinlärning** | En typ av ML som använder stora neurala nät, t.ex. för bildigenkänning eller röst-till-text. | Tekniken under huven i LLM:er, bildgeneratorer och andra “tunga” AI-funktioner som ofta körs på GPU. |
| **LLM (Large Language Model)** | Modeller som ChatGPT – läser och skriver text på ett sätt som upplevs som mänskligt. | Motorn bakom chat-assistenter, auto-sammanfattningar, generering av mejl, aktivitetsbeskrivningar, kod m.m. |
| **Generativ AI** | AI som skapar nytt innehåll – text, bilder, musik, video, kod. | Alla funktioner där användaren matar in några ord/punkter och får ett nytt innehåll tillbaka, t.ex. förslag på inlägg eller nyheter. |
| **Chatbot** | En chattande assistent på webben eller i en app. | Ett gränssnitt mot en LLM där du styr kontext, regler och begränsningar (t.ex. vad boten får och inte får svara på). |

---

## 2. Språk, prompts och kontext

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **Prompt** | Texten du skriver till en AI, t.ex. “Skriv ett mejl som…”. | All input du skickar till modellen – användarens text plus dold “systemtext” som styr beteendet. |
| **Prompt engineering** | Konsten att formulera frågor/uppdrag så att AI:n ger bra, användbara svar. | Design av stabila prompt-mallar som kan återanvändas i kod, t.ex. “skriv aktivitetsbeskrivning i enkel svenska utifrån dessa punkter”. |
| **Systemprompt** | Osynlig instruktion som berättar för modellen “vem” den ska vara (t.ex. lärare, coach). | Den statiska prompten du bakar in i backend som definierar roll, ton och regler: t.ex. “Du hjälper ideella föreningar att skriva tydlig, inkluderande text”. |
| **Context / Kontext** | Extra info du ger AI:n: bakgrund, tidigare chatt, exempel. | Text och data du skickar med i varje anrop (t.ex. info om föreningen, aktuella aktiviteter) så att svaret blir specifikt och korrekt. |
| **Token** | Små textbitar (delar av ord) som modellen arbetar med. | Viktigt för att förstå längdbegränsningar och kostnader – fler tokens = mer kontext och/eller längre svar, men också högre kostnad och längre svarstid. |
| **Context window** | Hur mycket modellen kan “ha i huvudet” samtidigt. | Max antal tokens per anrop; avgör hur många dokument, meddelanden eller datapunkter du kan skicka med i en prompt. |

---

## 3. Data, modeller och träning

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **Dataset** | En samling data – t.ex. alla aktiviteter under ett år eller alla mejl i en kampanj. | Underlag för träning, test eller analys, eller för indexering i en sök-/RAG-lösning. |
| **Träning (Training)** | När AI:n “lär sig” mönster från data. | Tunga, resurskrävande körningar där modellens parametrar justeras. Görs oftast av leverantörer (OpenAI m.fl.); ni använder vanligen redan tränade modeller. |
| **Fine-tuning** | Efterjustering – göra en färdig modell extra bra på ett visst område eller en viss stil. | När ni vill att en modell ska skriva just som Katchapp/FVK/Medialabbet, baserat på egna exempel. Kräver planering kring data, kostnad och driftsättning. |
| **Inference** | Själva användningen av modellen – när du ställer en fråga och får svar. | Varje API-anrop från appen till modellen är inference; det är denna del ni betalar för per användning. |
| **Parametrar (i en modell)** | Modellens inre “inställningar” (vikter) som den lär sig. | Antalet parametrar påverkar ofta modellens kapacitet, minneskrav och hastighet. Viktigt när man väljer mellan små lokala modeller och stora molnmodeller. |

---

## 4. Sök, embeddings och RAG

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **Embedding** | Ett sätt att göra om text till en sifferlista (vektor) så att AI kan mäta hur lika två texter är. | Används för smart sök – hitta liknande dokument, frågor eller aktiviteter baserat på betydelse och inte bara exakta ord. |
| **Vektor-databas** | En databas som lagrar embeddings och kan hitta “närmsta grannar” (mest liknande texter). | Byggblock för RAG: ni kan lagra föreningens dokument och låta modellen slå upp relevanta bitar inför varje svar. |
| **RAG (Retrieval-Augmented Generation)** | Teknik där AI först hämtar fakta från en källa och sedan skriver ett svar utifrån det. | Viktig om ni vill att AI-funktioner ska svara utifrån Katchapps/FVK:s egna dokument, istället för att hitta på eller använda allmän nätkunskap. |
| **Hallucination** | När AI hittar på saker som låter trovärdiga men är fel. | En central risk – särskilt om modellen inte får rätt kontext. Därför behövs RAG, tydliga begränsningar och mänsklig kontroll vid känsliga användningsfall. |

---

## 5. Infrastruktur, API och prestanda

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **API (Application Programming Interface)** | Ett sätt för program att prata med varandra – t.ex. en app som skickar text till en AI-tjänst och får svar tillbaka. | Katchapp eller utvecklingsverktyg kallar AI-modeller via HTTP-anrop, oftast JSON-baserade API:er. |
| **Endpoint** | En specifik “adress” i ett API där du kan göra en viss typ av anrop. | T.ex. `/chat/completions` för text, `/images` för bild. Varje endpoint har sina parametrar och begränsningar. |
| **Latency (Fördröjning)** | Tiden det tar från att du skickar något tills du får svar; upplevs som “segt” eller “snabbt”. | Påverkar användarupplevelsen. Beror på modellstorlek, nätverk, mängd kontext och var modellen körs (lokalt/moln). |
| **GPU (Grafikprocessor)** | Grafikkort – ofta för spel, men också viktigt för AI. | Används vid träning och ibland inference av modeller lokalt (t.ex. på en server som *nasty-render*). Moln-API:er döljer detta, men kostnaden speglar GPU-användning. |
| **Molntjänst / Cloud** | När beräkning och lagring sker på servrar online istället för på din egen dator. | De flesta AI-API:n är molnbaserade. Katchapp kan även köras i molnet, medan utvecklingsmiljöer kan vara lokala eller hybrida. |

---

## 6. Ansvar, etik och säkerhet

| Begrepp | Vardag | App-utveckling |
|--------|--------|----------------|
| **Bias** | Snedvridningar eller fördomar i AI:ns svar, t.ex. att vissa grupper framställs stereotypt. | Extra viktigt när målgruppen är sårbar (t.ex. psykisk ohälsa). Svar måste granskas och riktlinjer tas fram för ton och innehåll. |
| **Säkerhet (Security)** | Skydd mot obehörig åtkomst, dataläckor och sabotage. | API-nycklar, användardata och interna dokument måste hanteras säkert. AI-tjänster ska bara få den data de behöver. |
| **Integritet / Privacy** | Hur personuppgifter hanteras enligt lagar som GDPR. | Ni måste veta vilken data som skickas till AI-tjänster, vilka som är personuppgifter och hur länge den lagras. |
| **Anonymisering** | Att ta bort eller ändra personuppgifter så att individen inte kan identifieras. | Viktigt när ni vill använda verkliga texter/loggar som underlag för AI utan att röja identiteter. |

---

## 7. AI-agenter och orkestrering

| Begrepp | Vardag | App-utveckling / infrastruktur |
|--------|--------|--------------------------------|
| **AI-agent** | En mer “självgående” AI som inte bara svarar på en fråga, utan försöker uppnå ett mål genom flera steg. | En LLM som får ett uppdrag (t.ex. “sätt upp en ny microservice”) och kan planera delsteg, använda verktyg (API:er, filsystem, Git) och uppdatera sin plan under tiden. |
| **Verktyg / Tools (Tool calling)** | Sätt för agenten att göra saker utanför ren text, t.ex. kolla vädret eller läsa en fil. | Funktioner ni exponerar för agenten: “kör Git-kommando”, “generera Docker-fil”, “läs teknisk spec från repo”, “skapa pull request”. Plattformar som Flowise låter dig definiera sådana verktyg. |
| **Orkestrering** | Att styra flera delar så de spelar ihop – som en dirigent för en orkester. | Lagret som bestämmer när och hur agenter körs, vilka verktyg de får använda, hur fel hanteras och hur resultatet skickas vidare (t.ex. till CI/CD eller utvecklaren). |
| **Workflow / Flöde** | En kedja av steg: “gör A, sen B, sen C”. | En definierad kedja av AI- och verktygsanrop, t.ex. “1) läs teknisk spec → 2) generera kod → 3) kör tester → 4) skapa PR”. I grafiska verktyg (Flowise m.fl.) representeras detta som noder som kopplas ihop. |
| **Node / Block** | En “ruta” i ett visuellt arbetsflöde som gör en sak. | Byggsten i ett orkestreringsverktyg: en node kan vara ett LLM-anrop, en HTTP-förfrågan, ett filsystemsteg eller en databasaktion. |
| **Multi-agent system** | Flera AI-agenter som samarbetar eller har olika roller. | T.ex. en Arkitekt-agent (tolkar krav), en Kod-agent (skriver kod) och en Test-agent (kör tester). Orkestreringen styr i vilken ordning och med vilken kontext de körs. |
| **Planner / Planerande agent** | Den som först gör en plan innan arbetet startar. | En agent som tar ett övergripande mål (t.ex. “sätt upp ny utvecklingsmiljö för Katchapp”) och bryter ned det i konkreta deluppgifter som andra agenter eller verktyg ska utföra. |
| **Executor / Utförande agent** | Den som genomför själva arbetet enligt planen. | En agent som tar en deluppgift (“generera Docker-compose för tjänst X”) och utför den med hjälp av verktyg – t.ex. genererar filer, kör kommandon, uppdaterar Git. |
| **Minne (Memory)** | Agentens förmåga att minnas vad som hänt tidigare. | Lagring av konversationer, beslut, kodförändringar och loggar så att agenten kan ta hänsyn till historik vid nya uppgifter. Kan vara enkel historik eller mer avancerat vektor-baserat minne. |
| **Agent-ramverk (Agent framework)** | Ett paket/verktyg som gör det lättare att bygga agenter. | Exempel: Flowise, dev-gpt-liknande lösningar, LangChain, Semantic Kernel. Hjälper till att definiera verktyg, minne, roller, flöden och koppling till LLM-API:er. |
| **Orchestration layer / Orkestreringslager** | “Nervsystemet” som håller ihop alla delar. | Det lager (ibland en separat tjänst) som styr vilken agent som körs, när, med vilket underlag och vad som händer med resultatet (loggas, skickas till utvecklare, triggar nästa steg osv.). |
| **Human-in-the-loop (HITL)** | När en människa godkänner eller justerar innan AI:ns förslag används på riktigt. | Viktigt i utvecklingsflödet: t.ex. agenten får skapa kod eller PR, men en utvecklare måste granska innan det mergas eller rullas ut i drift. |
| **Guardrails** | Räcken som hindrar dig från att köra i diket. | Regler och tekniska begränsningar som bestämmer vad agenter får göra: vilka kommandon de får köra, vilka kataloger/system de får nå, och vilka svar som blockeras eller filtreras. Avgörande för säker användning av agenter i infrastruktur och system. |

---
