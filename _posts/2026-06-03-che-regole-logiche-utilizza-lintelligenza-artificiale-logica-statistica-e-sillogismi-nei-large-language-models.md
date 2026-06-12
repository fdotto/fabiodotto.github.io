---
layout: post
title: "Che regole logiche utilizza l’intelligenza artificiale? Logica, statistica e sillogismi nei Large Language Models"
date: 2026-06-03 12:46:50 +0200
categories: [ricerca]
tags: [AI, LLM, logica]
math: true
description: "I Large Language Models non ragionano con la logica formale: apprendono pattern di inferenza dai dati. Un’analisi di sillogismi, predizione statistica e limiti cognitivi dei modelli linguistici."
---

## Executive summary

Questo saggio analizza in che senso i Large Language Models (LLM) «usano la logica» quando producono inferenze, con particolare attenzione ai sillogismi classici e alla distinzione tra ragionamento deduttivo e predizione statistica di token. Viene mostrato che i LLM non implementano un motore logico simbolico separato, ma apprendono pattern di ragionamento a partire da dati testuali, cosicché in molti casi la conclusione logicamente valida coincide con il completamento statisticamente più probabile, mentre in altri casi si osservano errori sistematici e bias umani.[^1][^2][^3][^4]

L’analisi ricostruisce: (1) la nozione classica di ragionamento logico in AI simbolica; (2) il funzionamento dei modelli linguistici neurali e il loro carattere «statistico»; (3) l’evidenza empirica sulle prestazioni sillogistiche dei LLM; (4) i limiti attuali e i tentativi di integrazione neuro‑simbolica per ottenere capacità deduttive più robuste. Un esame conclusivo valuta criticamente l’idea che «la logica sia emersa dal training come pattern altamente affidabile», mostrando in che senso tale enunciazione è corretta e in che senso è fuorviante.[^5][^6][^7][^8][^9]

## Capitolo 1 – Logica formale e ragionamento in AI simbolica

### 1.1. Obiettivo del capitolo

Questo capitolo chiarisce che cosa significhi, in informatica e in logica, dire che un sistema «usa regole logiche», ricostruendo il paradigma dell’AI simbolica (o GOFAI) e il suo rapporto con la logica del prim’ordine. Ciò fornisce il termine di paragone necessario per valutare il comportamento dei LLM.[^7][^10]

### 1.2. Regole logiche, validità e deduzione

Nella tradizione logica, una regola di inferenza specifica quando da certe premesse è lecito derivare una conclusione, indipendentemente dal contenuto lessicale. Per esempio, il sillogismo «Tutti gli uomini sono mortali; Socrate è un uomo; dunque Socrate è mortale» è valido perché istanzia uno schema di inferenza corretto.[^7]

Nella notazione della logica del prim’ordine, lo schema sottostante può essere reso come:

- Premessa maggiore: \(\forall x( U(x) \rightarrow M(x))\) (per ogni x, se x è un uomo allora x è mortale)
- Premessa minore: \(U(s)\) (Socrate è un uomo)
- Conclusione: \(M(s)\) (Socrate è mortale)

La regola utilizzata è il modus ponens, che consente di passare da \(P\) e \(P \rightarrow Q\) a \(Q\) in modo puramente formale, senza considerare frequenze o probabilità. La proprietà centrale è la *necessità* della conclusione: dato che le premesse sono vere e la forma è valida, la conclusione non può essere falsa.[^7]

### 1.3. AI simbolica, basi di conoscenza e motori inferenziali

L’AI simbolica classica rappresenta la conoscenza mediante formule logiche e applica regole d’inferenza per derivare nuove informazioni. Una base di conoscenza contiene fatti (per esempio `uomo(Socrate)`) e regole (`∀x(uomo(x) → mortale(x))`), mentre un motore inferenziale (inference engine) implementa sistematicamente le regole, ad esempio tramite dimostrazione per risoluzione o calcolo dei sequenti.[^8][^10]

In un sistema del genere, la conclusione «Socrate è mortale» viene ottenuta cercando una dimostrazione formale a partire dalle premesse. Le proprietà rilevanti sono:[^8]

- Correttezza: tutto ciò che viene dimostrato è semanticamente valido.
- Completezza (in vari sistemi logici classici): tutto ciò che è semanticamente valido è dimostrabile.
- Trasparenza: la sequenza di passi inferenziali è esplicita e ispezionabile.

Questi tratti costituiranno il contrasto principale con il comportamento dei LLM, che non possiedono rappresentazioni simboliche esplicite né motori di dimostrazione dedicati.

## Capitolo 2 – Modelli linguistici neurali e natura statistica della predizione

### 2.1. Obiettivo del capitolo

Questo capitolo descrive a livello concettuale come funzionano i modelli linguistici neurali di tipo transformer, chiarendo perché si parla di «predizione statistica di token» anziché di deduzione logica esplicita.[^3][^4]

### 2.2. Trasformers, attenzione e predizione di token

I moderni LLM (GPT, PaLM, Claude, ecc.) sono reti neurali profonde addestrate a predire, dato un contesto testuale, la distribuzione di probabilità sui possibili token successivi. L’architettura transformer utilizza meccanismi di attenzione per combinare in modo contestuale le rappresentazioni vettoriali di tutte le parole precedenti, producendo un vettore da cui viene calcolata una distribuzione di probabilità via softmax.[^3]

Formalmente, il modello implementa una funzione che associa a una sequenza di token \(w_1,\dots,w_n\) una distribuzione condizionale \(p(\cdot \mid w_1,\dots,w_n)\). L’addestramento consiste nel massimizzare la verosimiglianza dei dati osservati, cioè nel rendere elevata la probabilità dei token che effettivamente seguono nei testi del corpus.[^3]

### 2.3. L’interpretazione come kernel di Markov finito ordine

Una recente analisi concettuale suggerisce di interpretare un LLM come un kernel di Markov di ordine finito che mappa contesti linguistici in distribuzioni di token, senza implementare esplicitamente strutture logiche o operatori deduttivi. In questo quadro, le «catene di ragionamento» generate dal modello sono sequenze di token che rispecchiano regolarità statistiche apprese, non l’esecuzione di un algoritmo logico interno.[^5][^3]

Gli autori sottolineano che tale prospettiva chiarisce perché i LLM possano produrre testi che sembrano ragionamenti, pur senza offrire garanzie di coerenza logica globale: la coerenza emerge solo nella misura in cui è stata «statisticamente premiata» nei dati di addestramento.[^5]

### 2.4. Ragionamento come pattern emergente

Numerosi studi empirici mostrano che, all’aumentare della scala del modello e della quantità di dati, emergono capacità di risoluzione di compiti che richiedono parecchi passaggi di ragionamento (calcolo aritmetico, problemi logici, dimostrazioni schematiche). Tali capacità non derivano da un modulo logico progettato a priori, ma dall’auto‑organizzazione della rete nel catturare regolarità composizionali del linguaggio e del discorso argomentativo.[^11][^4]

Da questo punto di vista, è plausibile dire che «la logica emerge come pattern altamente affidabile» in certi domini (ad esempio i sillogismi standard) perché nei corpora abbondano esempi di inferenze corrette, il cui schema formale diventa fortementemente probabile. Tuttavia ciò non implica l’esistenza di una rappresentazione interna delle regole logiche nei termini usuali della logica matematica.[^4][^11]

## Capitolo 3 – Sillogismi classici: come si comportano i LLM?

### 3.1. Obiettivo del capitolo

Questo capitolo esamina la letteratura recente sul comportamento dei LLM in compiti sillogistici controllati, confrontandoli con esseri umani e con i criteri della logica formale.[^12][^13][^1]

### 3.2. Studi sistematici sui sillogismi

Una serie di lavori recenti ha valutato in modo sistematico la capacità di vari LLM (es. la famiglia PaLM 2) di risolvere sillogismi categoriali, confrontando le risposte con la validità logica e con le prestazioni umane. I risultati mostrano che:[^12][^1]

- I modelli più grandi tendono a commettere meno errori rispetto ai modelli piccoli e, in alcuni benchmark, risultano più «logici» della media dei partecipanti umani.[^1]
- Tuttavia, permangono errori sistematici, inclusi fallacie sillogistiche note (come affermazione del conseguente o conclusioni non licite da premesse particolari).[^2]

Un ulteriore studio utilizza il fenomeno dell’«importo esistenziale» per sondare se i modelli adottino implicitamente la logica tradizionale aristotelica o la logica moderna del prim’ordine quando valutano sillogismi con termini vuoti. L’evidenza suggerisce che l’aumento di scala del modello e l’uso di tecniche di «thinking» (prompting che induce ragionamento esplicito) promuovono un comportamento più vicino alla logica moderna.[^13]

### 3.3. Bias umani e ordine delle premesse

Gli stessi studi segnalano che i LLM possono manifestare bias analoghi a quelli umani, come la sensibilità all’ordine di presentazione delle premesse, nonostante la validità logica non dipenda da tale ordine. Ad esempio, alcuni modelli mostrano una maggiore propensione a inferenze corrette quando la premessa generale precede quella particolare rispetto al caso inverso.[^2][^1]

Questo fenomeno indica che il modello non opera su una rappresentazione astratta dell’argomento, ma è influenzato da correlazioni superficiali apprese nei dati linguistici (ad esempio, la frequente presentazione dei sillogismi da parte generale a particolare). Analogamente, si osservano casi in cui la plausibilità semantica del contenuto (belief bias) interferisce con il rispetto della forma logica, sia nei soggetti umani sia nei LLM.[^14][^1]

### 3.4. Interpretazione dei risultati

Taken insieme, questi risultati supportano una tesi intermedia: i LLM non sono meri «pappagalli stocastici», ma acquisiscono una forma di competenza strutturale che li rende capaci di applicare pattern inferenziali relativamente astratti, soprattutto quando adeguatamente «guidati» dal prompting. Al contempo, l’assenza di un motore logico esplicito comporta che tali pattern restino fallibili, influenzati da bias di frequenza e plausibilità.[^11][^1]

Per la domanda «la conclusione logicamente valida è anche la più probabile?», gli studi mostrano che spesso è così nei casi canonici, ma non in quelli rari, contro‑intuitivi o costruiti apposta per disaccoppiare validità e plausibilità.[^15][^14][^12]

## Capitolo 4 – Analisi dell’affermazione: «la conclusione logicamente valida è anche la più probabile»

### 4.1. Obiettivo del capitolo

Questo capitolo analizza filosoficamente l’affermazione secondo cui, per i LLM, la conclusione logicamente valida coincide con il completamento più probabile, discutendo in quali condizioni ciò accade e in quali fallisce.[^15][^1][^5]

### 4.2. Il caso paradigmatico: sillogismi standard

Per sillogismi altamente frequenti nei testi (come l’esempio con Socrate), il modello ha visto numerose istanze in cui alla coppia di premesse segue la conclusione corretta. Di conseguenza, lo schema «tutti X sono Y; Z è X → Z è Y» diventa fortemente radicato nella distribuzione appresa: date le due premesse, la stringa «dunque Z è Y» e sue varianti è tipicamente ad altissima probabilità condizionale.[^15]

In tali casi, si può dire che il modello «riconosce lo schema» nel senso che la combinazione di pattern sintattico («tutti X sono Y») e semantico («X è una sottoclasse di Y») è stata associata, in fase di training, a continuazioni che esprimono proprio la conclusione logica. Formalmente, tuttavia, non esiste un livello in cui la formula universale e l’istanza vengono manipolate come simboli discreti secondo regole logiche.[^12][^1]

### 4.3. Divergenza tra logica e probabilità

La tesi che la conclusione logicamente valida sia anche la più probabile fallisce quando i corpus contengono pochi esempi dello schema in questione, oppure quando i dati privilegiano sistematicamente inferenze scorrette ma plausibili. Studi psicologici sui LLM riportano difficoltà con sillogismi rari, composizioni logiche non standard e situazioni in cui la plausibilità semantica suggerisce una conclusione, ma la forma logica ne richiede un’altra.[^14][^12][^5][^15]

Un caso tipico è quello dei syllogistic fallacies: i modelli, come gli umani, possono essere indotti ad affermare una conclusione non valida perché essa appare più «ragionevole» alla luce delle credenze di sfondo implicite nel testo, pur non seguendo dalle premesse secondo le regole della logica classica. In questi casi, la conclusione logicamente corretta può avere probabilità condizionale inferiore rispetto alla conclusione intuitiva ma scorretta.[^1][^14]

### 4.4. Premesse false, forma logica e correzione automatica

Un’altra divergenza riguarda il trattamento di premesse intenzionalmente false ma formalmente ben formate. È stato osservato che i LLM tendono talvolta a «correggere» o reinterpretare premesse assurde per riportarle entro un quadro di plausibilità, invece di attenersi rigidamente alla forma logica e trarne conseguenze paradossali.[^16][^5]

Questo comportamento deriva dal fatto che il modello è stato addestrato a continuare testi realistici o simili a quelli umani medi, non a perseguire conseguenze logiche a partire da premesse arbitrariamente scelte. Di conseguenza, l’algoritmo interno favorisce continuazioni che mantengano coerenza semantica globale rispetto alle statistiche del corpus, anche a costo di «tradire» la pura forma logica richiesta da un esercizio filosofico o matematico.[^5]

## Capitolo 5 – Chain-of-thought, ragionamento passo‑passo e loro limiti

### 5.1. Obiettivo del capitolo

Questo capitolo discute il ruolo delle tecniche di *chain‑of‑thought prompting* (CoT) nel migliorare la performance logica dei LLM e in che senso queste tecniche avvicinino il comportamento del modello a una deduzione esplicita.[^17][^4][^11]

### 5.2. Chain-of-thought prompting

Il *chain‑of‑thought prompting* è una tecnica in cui, invece di chiedere direttamente la risposta, si induce il modello a generare una serie di passaggi intermedi di ragionamento in linguaggio naturale, spesso mediante esempi o tramite istruzioni («pensiamo passo per passo»). Gli esperimenti mostrano che questo tipo di prompting migliora sensibilmente le prestazioni su compiti aritmetici, logici e di ragionamento simbolico.[^4][^11]

Wei e colleghi hanno evidenziato che tali benefici emergono solo per modelli di scala sufficiente (dell’ordine di centinaia di miliardi di parametri), suggerendo che la capacità di mantenere e manipolare strutture di pensiero multi‑passo è un’abilità emergente. In termini funzionali, il CoT costringe il modello ad esplicitare gli stessi pattern inferenziali che altrimenti rimarrebbero compressi nello spazio vettoriale.[^11][^4]

### 5.3. CoT come «simulazione» di deduzione

Da un punto di vista logico, il CoT non trasforma il LLM in un dimostratore formale, ma lo induce a riprodurre, in linguaggio naturale, tracce di ragionamento simili a quelle che un agente deduttivo potrebbe seguire. La correttezza di queste tracce non è garantita a priori, ma può essere valutata ex post, e strategie come la *self‑consistency* (generare molte catene e fare voto di maggioranza) innalzano ulteriormente l’accuratezza.[^17][^4][^11]

Questo supporta una lettura secondo cui il LLM agisce come un simulatore di «ragionatori testuali»: data una domanda, produce la continuazione che massimizza la probabilità congiunta di una certa narrazione argomentativa e di una risposta finale corretta, quando nel corpus vi sono esempi analoghi. L’aspetto deduttivo resta quindi «simulato» mediante pattern linguistici piuttosto che realizzato mediante regole logiche interne.[^11][^5]

### 5.4. Limiti delle tecniche CoT

Malgrado i progressi, gli studi evidenziano che il CoT non elimina bias sistematici né misconcezioni logiche profonde. Alcuni errori sono semplicemente spostati dal livello della risposta finale al livello della catena di ragionamento, che può contenere passaggi scorretti ma plausibili.[^17][^11]

Inoltre, la produzione di lunghe catene aumenta il rischio di «deriva» discorsiva, introducendo confabulazioni o passaggi non strettamente necessari alla soluzione logica. Per quanto il CoT avvicini il comportamento esterno del modello a quello di un ragionatore che segue una prova, la differenza ontologica rispetto a un sistema logico‑deduttivo basato su regole rimane netta.[^17]

## Capitolo 6 – Neuro‑symbolic AI: integrare logica e apprendimento

### 6.1. Obiettivo del capitolo

Questo capitolo presenta, in forma sintetica, l’area della Neuro‑symbolic AI, che mira a combinare i punti di forza dei modelli neurali (apprendimento da dati) con quelli dei sistemi simbolici (ragionamento logico esplicito).[^18][^6][^19]

### 6.2. Motivazioni per un’integrazione

I limiti dei LLM in termini di coerenza logica globale, verificabilità e affidabilità per applicazioni critiche hanno spinto verso architetture ibride in cui moduli logici espliciti cooperano con reti neurali. In tali sistemi, la rete neurale funge spesso da modulo percettivo o di estrazione di pattern, mentre un livello simbolico esegue ragionamenti basati su regole (per esempio usando logica proposizionale o logica del prim’ordine).[^6][^18]

Questa integrazione può affrontare problemi di data efficiency, fairness e sicurezza, offrendo spiegazioni sotto forma di prove o derivazioni logiche. Inoltre, consente di incorporare conoscenza di dominio pre‑esistente (per esempio ontologie o knowledge graph) che sarebbe difficile apprendere solo dai dati.[^19][^6]

### 6.3. Esempi di approcci neuro‑simbolici

La letteratura propone vari schemi di integrazione, tra cui: reti neurali che approssimano la soddisfacibilità di formule logiche mediante funzioni di energia; architetture che vincolano l’addestramento con regole «if‑then» espresse in logica; sistemi gerarchici in cui un pianificatore simbolico ad alto livello guida un controller neurale a basso livello.[^20][^18][^6]

In alcuni casi si dimostra formalmente che il sistema neurale può rappresentare e ragionare su qualsiasi formula proposizionale, collegando la minimizzazione dell’energia a processi di ricerca di modelli o di risoluzione di problemi SAT. Tali sistemi costituiscono esempi genuini di ragionamento logico implementato in una struttura neurale, ma a prezzo di un design mirato molto diverso dall’addestramento general‑purpose dei LLM.[^6]

## Capitolo 7 – Valutazione critica della risposta proposta

### 7.1. Obiettivo del capitolo

Questo capitolo mette in dialogo la letteratura esaminata con la formulazione: «l’AI non ha un motore logico‑deduttivo separato, ma durante il training ha visto miliardi di esempi di ragionamento corretto, quindi la conclusione logicamente valida è anche la staticamente più probabile. (…) non c’è un “modulo logico”, ma la logica è emersa dal training come pattern altamente affidabile».

### 7.2. Parti confermate dalla letteratura

Le evidenze empiriche e le analisi concettuali confermano che i LLM standard non includono un modulo logico simbolico separato paragonabile a un teorema‑prover o a un calcolo dei sequenti; essi operano come modelli generativi neurali che apprendono distribuzioni di token. Inoltre, numerosi risultati mostrano che, in compiti ben rappresentati nei dati (sillogismi canonici, problemi aritmetici di base), i modelli tendono a produrre inferenze logicamente corrette con alta affidabilità, in parte perché tali inferenze corrispondono alle continuazioni statisticamente dominanti nei corpora.[^12][^1][^3][^5][^11]

Anche l’idea che la «logica emerga come pattern» è in linea con la visione secondo cui i LLM implementano un kernel statistico che approssima invarianti strutturali nei dati linguistici, tra cui schemi inferenziali come modus ponens e sillogismi categoriali.[^21][^5]

### 7.3. Punti problematici e precisazioni

Tuttavia, la tesi secondo cui «la conclusione logicamente valida è anche la più probabile» deve essere intesa con forte cautela e con molte riserve. La letteratura sui sillogismi e sui bias mostra numerosi casi in cui i LLM preferiscono conclusioni plausibili ma non valide, oppure in cui la conclusione corretta è scelta solo con bassa probabilità o sotto specifiche condizioni di prompting.[^14][^15][^12]

Inoltre, l’affermazione può suggerire, impropriamente, che il modello abbia «visto miliardi di esempi di ragionamento corretto» e quindi appreso «la logica in generale»; in realtà, la distribuzione dei casi nei corpora è fortemente sbilanciata, e per molte forme logiche sofisticate (ad esempio ragionamenti quantificazionali complessi, dimostrazioni matematiche astratte) i dati potrebbero essere relativamente scarsi o rumorosi.[^21][^5]

Infine, la stessa idea di «pattern altamente affidabile» va relativizzata: la robustezza logica dei LLM crolla spesso quando si esce dal regime IID dei benchmark standard, ad esempio in presenza di avversarial examples, composizione ricorsiva profonda o premesse intenzionalmente assurde. In queste situazioni, un sistema logico simbolico mantiene la validità delle regole, mentre il LLM può deviare sensibilmente.[^13][^5]

### 7.4. Risposta alla domanda: il modello «ragiona» o solo predice?

Gli studi portano verso una posizione intermedia: dal punto di vista implementativo, i LLM sono predittori statistici di token; dal punto di vista comportamentale, in molti casi manifestano strutture di risposta che soddisfano criteri operativi di ragionamento, soprattutto se guidati da tecniche come il chain‑of‑thought.[^4][^5][^11]

In particolare, nel caso del sillogismo «tutti gli uomini sono mortali; Socrate è un uomo», il modello genera tipicamente «Socrate è mortale» perché questa continuazione massimizza una distribuzione appresa che, per via dei dati, codifica implicitamente lo schema inferenziale corrispondente; ma ciò non implica l’esecuzione consapevole di una regola logica interna. Si può dire che il modello *simula* il ragionamento sillogistico, piuttosto che instanziarlo nel senso classico della logica matematica.[^1][^12]

## Capitolo 8 – Conclusioni aperte

### 8.1. Sintesi dei risultati

Il confronto tra AI simbolica, LLM e Neuro‑symbolic AI suggerisce che le «regole logiche» nei modelli linguistici contemporanei non sono entità primitive ma regolarità emergenti in una dinamica di apprendimento statistico su larga scala. Quando i dati sono favorevoli, queste regolarità coincidono con schemi logici standard, producendo inferenze che, a tutti gli effetti pratici, sono valide; quando dati e bias remano contro, la divergenza tra logica e probabilità diventa evidente.[^6][^3][^14][^12][^5][^1]

L’evoluzione verso architetture neuro‑simboliche indica una possibile via per dotare i sistemi di capacità deduttive con garanzie formali, mantenendo al contempo la flessibilità dei modelli neurali. Il dibattito filosofico rimane aperto su come interpretare concetti come «ragionamento», «comprensione» e «logica» in sistemi che, pur essendo statisticamente addestrati, producono prestazioni sempre più vicine a quelle di agenti razionali ideali.[^18][^19][^6]

### 8.2. Implicazioni per la ricerca futura

Dal punto di vista logico‑filosofico, la sfida è articolare criteri più fini per distinguere tra simulazione e implementazione del ragionamento, forse scomponendo «logica» in dimensioni multiple (validità formale, consapevolezza metariflessiva, capacità di revisione delle credenze, ecc.). Dal punto di vista informatico, restano centrali i problemi di valutare sistematicamente la robustezza logica dei LLM al di fuori dei benchmark standard e di progettare architetture ibride che coniughino prove formali e apprendimento.[^21][^5]

In questo senso, la domanda iniziale «che regole logiche utilizza l’intelligenza artificiale?» potrebbe essere riformulata così: *in quali condizioni le regolarità statistiche apprese dai modelli neurali coincidono con le regole della logica formale, e come possiamo progettare sistemi in cui tale coincidenza sia garantita e non soltanto contingente ai dati di addestramento?*[^6][^5]

---

## References

1. [A Systematic Comparison of Syllogistic Reasoning in ...](https://aclanthology.org/2024.naacl-long.466/) - Tiwalayo Eisape, Michael Tessler, Ishita Dasgupta, Fei Sha, Sjoerd Steenkiste, Tal Linzen. Proceedin...

2. [A Systematic Comparison of Syllogistic Reasoning in ...](https://openreview.net/forum?id=4bUeP3qrNu) - A central component of rational behavior is logical inference: the process of determining which conc...

3. [On the Notion that Language Models Reason](https://arxiv.org/html/2511.11810v1)

4. [Language Models Perform Reasoning via Chain of Thought](https://research.google/blog/language-models-perform-reasoning-via-chain-of-thought/) - Posted by Jason Wei and Denny Zhou, Research Scientists, Google Research, Brain team In recent years...

5. [Paper page - On the Notion that Language Models Reason](https://huggingface.co/papers/2511.11810) - Join the discussion on this paper page

6. [[2505.20313] Reasoning in Neurosymbolic AI - arXiv](https://arxiv.org/abs/2505.20313) - Knowledge representation and reasoning in neural networks have been a long-standing endeavor which h...

7. [Knowledge Representation and Reasoning - Google Books](https://books.google.com/books/about/Knowledge_Representation_and_Reasoning.html?id=OuPtLaA5QjoC) - This book provides the foundation in knowledge representation and reasoning that every AI practition...

8. [How do symbolic reasoning models work?](https://milvus.io/ai-quick-reference/how-do-symbolic-reasoning-models-work) - Symbolic reasoning models operate by manipulating structured representations of knowledge using pred...

9. [Symbolic AI vs. Statistical AI](https://www.ultralytics.com/glossary/symbolic-ai) - Explore Symbolic AI and its role in logical reasoning. Learn how to combine logic-based GOFAI with U...

10. [Knowledge representation and reasoning by Ronald J. Brachman](https://openlibrary.org/books/OL19149301M/Knowledge_representation_and_reasoning) - This book provides the foundation in knowledge representation and reasoning that every AI practition...

11. [Chain-of-Thought Prompting Elicits Reasoning in Large Language ...](https://arxiv.org/abs/2201.11903) - We explore how generating a chain of thought -- a series of intermediate reasoning steps -- signific...

12. [Under review as a conference paper at ICLR 2024](https://openreview.net/pdf?id=4bUeP3qrNu)

13. [A Syllogistic Probe: Tracing the Evolution of Logic Reasoning in Large Language Models](https://www.arxiv.org/abs/2601.17426) - Human logic has gradually shifted from intuition-driven inference to rigorous formal systems. Motiva...

14. [Understanding Syllogistic Reasoning in LLMs from Formal and ...](https://arxiv.org/html/2512.12620v1)

15. [Summary: The text suggests that Large Language Models (LLMs) base their reasoning on statistical probability rather than logic. This statistical reasoning often fails in less common scenarios. The discussion then questions the future development of truly logical AI, contrasting mathematical logic with philosophical logic, and wonders if LLMs might one day mimic logical reasoning so well that they seem logical, despite not being inherently so. The text also questions whether human reasoning is truly logical or just appears to be. - text.is](https://text.is/1V0OJ) - Summary: The text suggests that Large Language Models (LLMs) base their reasoning on statistical pro...

16. [Language Models are not Thinking Machines | Sabr Research](https://sabrresearch.com/blogs/llm-thinking) - When semantic prior overrides user constraints.

17. [Chain-of-Thought (CoT) Prompting](https://www.promptingguide.ai/techniques/cot) - A Comprehensive Overview of Prompt Engineering

18. [[PDF] HYBRID NEURO-SYMBOLIC REASONING BASED ON ...](https://openreview.net/pdf?id=SFyOjfEOJO)

19. [A review of neuro-symbolic AI integrating reasoning and ...](https://www.sciencedirect.com/science/article/pii/S2667305325000675)

20. [Hierarchical Neuro-Symbolic Decision Transformer](https://arxiv.org/html/2503.07148v2)

21. [Attention as Binding: A Vector-Symbolic Perspective on Transformer ...](https://arxiv.org/html/2512.14709v1)
