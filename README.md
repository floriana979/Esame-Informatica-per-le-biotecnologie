# ANALISI E VALIDAZIONE DI STRUTTURE MOLECOLARI FAME

# DESCRIZIONE GENERALE
   Il progetto permette l'analisi e la validazione di stringhe in formato FAME, un sistema di codifica per strutture molecolari.
   L'obiettivo principale è verificare se una data sequenza rispetti i vincoli chimici di valenza e le regole sintattiche di composizione.
   Il codice si basa du tre pilastri:
- definizione delle valenze atomiche standard (C,N,O,H,F,S) e dei pesi dei legami covalenti tramite strutture a dizionario
- scansione sequenziale della stringa per mappare i legami tra atomi, con gestione delle ramificazioni tramite un sistema di ancoraggio e indicatori di stato
- controllo finale dei legami di ogni singolo atomo, garantendo che l'intera struttura corrisponda a una molecola chimicamente valida.

# REGOLE DI INSERIMENTO
   il processo di validazione segue regole ben precise:
1. Unicità del Target:
       ogni atomo inserito deve avere un punto di ancoraggio (target) valido, a meno che non sia il primo atomo della stringa.
2. Vincolo di Ramificazione:
       una ramificazione deve essere aperta con ^ e chiusa con &. Non è consentito lasciare rami aperti o iniziare un ramo senza un atomo di supporto.
3. Esito dell'operazione:
       la validazione ha successo solo se la stringa termina con un atomo e non con un simbolo di legame
4. Saturazione obbligatoria:
       ogni atomo deve instaurare un numero di legami esattamente uguale alla sua valenza teorica: ne più, ne meno.
# STRUTTURA DEL CODICE
  il progetto è racchiuso nella funzione principale verifica_valenza_fame, suddivisa in
1. Modulo di inizializzaizone: configurazione delle valenze e dei pesi dei legami tramite dizionari
2. Motore di Parsing:un ciclo iterativo che scansiona la stringa e costruisce la mappa dei legami
3. Validazione finale: un sistema di controllo che verifica la chiusura delle strutture e il rispetto dei vincoli chimici

# FUNZIONE NEL DETTAGLIO
  la funzione verifica_valenza_fame() esamina la stringa molecolare per validare la struttura.
# 
 Parametri di Input
 - 
 - fame_stringa (str): la sequenza di atomi, legami e ramificazioni da analizzare
#
 Output
 - 
 - True: se la molecola rispetta tutte le regole sintattiche e le valenze chimiche
 - False: se vengono rilevati caratteri estranei, rami aperti, legami terminali o valenze errate

# DETTAGLIO PROCESSO DI ANALISI
 la funzione segue tre fasi sequenziali
1. Identicazione e collegamento:
   il sistema individua ogni carattere e aggiorna lo stato:
- Atomo: viene creato un ID unico e identificato il target se presente (ultimo atomo della catena o l'atomo ancora della ramificazione)
- Legame: viene memorizzato il valore del legame attuale per applicarlo alla connessione successiva
2. Gestione delle ramificazioni:
- al simbolo ^ --> ultimo atomo diventa ancora e il sistema entra in modalità ramificazione (in_ramificazione=True)
- al simbolo & --> il sistema esce dalla ramificazione (in_ramificazione=False) e resetta il target sulla catena principale
3. Verifica finale:
  si contorllano tutti i dati accumulati, e si devono verificare queste condizioni:
- in_ramificazione = False (indica che tutti i rami sono chiusi)
- legame_esplicito=False (indica che nessun legame è interrotto)
- si confronta somma_legami[i] con valenze[tipo_atomi[i]] per ogni atomo registrato


  
