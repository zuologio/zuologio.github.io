---
published: true
title: UWP CASE STUDY
layout: post
---
Il lancio di windows 10 durante l'estate 2015 è stato preceduto dalla promozione di una serie di strumenti per la creazione delle app che il nuovo sistema operativo avrebbe supportato: le "applicazioni universali". Il nome "Universal Windows Platform" di per se piuttosto altisonante si riferisce infatti al raggiungimento dell'obiettivo ambizioso di scrivere codice una sola volta per poi avere la propria app disponibile su tutti i device dotati di windows (10). Dopo anni di tentativi poco fortunati e di strumenti incompleti quello che avevano promesso dal lancio di windows 8 è stato finalmente possibile. 

Ho iniziato a giocare con windows 10 e le app universali 6 mesi prima del lancio al grande pubblico (utilizzando versioni insider e poi rc). Dopo i vari test "hello world" volevo trovare un progetto che "valesse la pena" di impegnare il mio tempo libero (principalmente le notti insonni passate con mia figlia nata da poco). 

Ho già fatto in passato app e/o siti web a titolo personale e i principali limiti che ho riscontrato sono:
- La necessità di manutenere l'hosting (configurare vm, db, iis, deploy, aggiornamenti vari dell'os, credenziali etc... tutta roba che dopo l'entusiasmo del lancio diventa presto una noia e probabile fonte di disservizio).
- La necessità di "promuovere" l'app. Ok, promuovere è una parola grossa, in ogni caso fare un'app al giorno d'oggi e non avere un sito per presentare l'app stessa non è concepibile. 

Ad un certo punto è arrivata l'idea: un sistema per caricare, utilizzando un device master, pagine web su device slave. L'idea di fondo era quella di creare uno strumento per agevolare la visualizzazione di contenuti web su device "particolari" (sprovvisti di tastiera e mouse). Windows 10 infatti gira su piattaforme molto interessanti tra cui, per citarne due a caso: raspberry pi 2 e xbox one che nei loro contesti applicativi non prevedono necessariamente la presenza di tastiera e mouse... 

Ho quindi strutturato l'app sviluppando tre componenti:
1) Un sito web di presentazione dell'app e che al tempo stesso è il backend per l'associazione degli url ai vari dispositivi dell'utente (ho usato un azure website).
2) Un'app universale che dopo il login si limita a mostrare l'url impostato dal sito.
3) Un layer di servizi utilizzato sia dall'app che dal sito (ho usato gli azure mobile services).

Ho infatti pensato di risolvere le debolezze con le quali mi ero scontrato in passato utilizzando windows azure: ho creato rapidamente il sito per la mia app e ho di fatto annullato tutti i problemi sistemistici dell'hosting tradizionale utilizzando il cloud!
Nello sviluppo ho scelto di usare Entity Framework 6.1 come orm e me ne sono innamorato (l'ultima mia esperienza era con la versione 4 e il suo odioso file edmx...). 

Ho pubblicato l'app nello store di microsoft pochi giorni dopo l'uscita ufficiale del'os! 
La prima versione si basava su un ciclo infinito in cui periodicamente l'app si incaricava di capire se l'url da visualizzare era cambiato oppure no. Dopo un po' ho rilasciato una nuova versione basasta sull'engine di push notifications messo a disposizione da azure. In questo modo la variazione dell'url sul sito viene notificata ai device senza che questi ultimi debbano costantemente interrogare il db (con conseguente aumento di performance, riduzione dell'utilizzo di batteria e dei tempi di aggiornamento dell'url). 

Windows 10 per xbox one deve ancora uscire (uscirà a breve), quindi il device più direttamente interessato dal mio progettino era il raspberry pi 2. Ho seguito il lancio di windows 10 iot con grande interesse. Ho inziato subito a provare il debug remoto della mia app all'intero della shell di questa particolare release di windows il cui limite principale è l'assenza dell'accesso allo store. Al fine di sopperire a questo limite ho creato un'immagine custom del sistema operativo con preinstallato il mio applicativo che parte automaticamente al termine della fase di boot (!). Ho quindi reso disponibile all'interno del sito della app il download dell'immagine custom di windows 10 iot completando l'offerta di microsoft al di fuori dello store.

Ho testato quindi la mia app su pc e su tv (con un raspberry collegato). La UI è dannatamente semplice e si basa principalmente su un form di login (centrato orizzontalmente e verticalmente) e su una webview che occupa il 100% della finestra. In questo modo, a prescindere dalla dimensione dello schermo, l'interfaccia dell'applicazione risulta sempre gradevole.  

Da fine ottobre 2015 ho chiuso, dopo aver implementato una serie di funzionalità minori, lo sviluppo di questo progetto. Ho visto e imparato un sacco... che l'app serva a qualcuno è oggettivamente secondario. Ho iniziato a fare altro.

Una settimana fa, dopo mesi di attesa ho ricevuto l'aggiornamento a windows 10 sul mio telefono. Ho scaricato subito la mia app e funziona divinamente. Le cose fatte bene sono ... "universali"!