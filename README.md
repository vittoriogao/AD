# Guida: Configurare Active Directory su Windows Server 2025

Benvenuto in questa guida passo passo su come installare e configurare Active Directory.

Il mio approccio scelto è stato tramite **PowerShell**, uno strumento più potente e rapido rispetto alla interfaccia grafica (GUI).

## Metodo 1: Installazione tramite PowerShell (Consigliato)

Questo metodo è il più veloce

### Passaggio 1: Installare il Ruolo Active Directory

  Collegati alla tua macchina Windows Server 2025. Apri una finestra di **PowerShell con privilegi di amministratore**.
   Lancia il seguente comando per installare i servizi di dominio e gli strumenti di gestione:

    Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools


  Al termine, vedrai un output simile a questo, che conferma il successo dell'operazione:
  
  <img width="992" height="176" alt="immagine" src="https://github.com/user-attachments/assets/3d58f085-01c4-4566-a7f8-4b8a965ba332" />

  (nel mio caso riporta NoChangeNeeded in quanto già presente ma se la colonna di Success è true allora ha avuto successo l'installazione)
 

 Ora lancia il comando per creare la nuova foresta. **Sostituisci i valori di esempio** con quelli desiderati.

    
    Install-ADDSForest `
        -DomainName "esempio" `
        -DomainNetbiosName "qua potrai cambiarlo in un nome più breve" `
        -InstallDns:$true `
        -ForestMode Win2025 `
        -DomainMode Win2025 `
        -SafeModeAdministratorPassword ( `
        -Force
   
 **Nota:** Dopo aver eseguito l'ultimo comando, il server verrà **riavviato** per completare la configurazione.

---

## Metodo 2: Installazione tramite Interfaccia Grafica (GUI)


- Se volessimo invece farlo da GUI:
   - tasto Start e cerchiamo Server Manager
  - Successivamente Aggiungi ruoli e funzionalità
  - 
  <img width="1022" height="429" alt="immagine" src="https://github.com/user-attachments/assets/1a05b9b7-3ee8-4e15-a306-0346ffa75482" />

- Premere avanti

<img width="773" height="546" alt="immagine" src="https://github.com/user-attachments/assets/301058c5-59da-484d-a0d4-7ac0aa5df5c4" />

<img width="787" height="555" alt="immagine" src="https://github.com/user-attachments/assets/2e97af59-b0ca-4f29-818a-8c92d6cab055" />

-  qua si seleziona il server
  
<img width="771" height="548" alt="immagine" src="https://github.com/user-attachments/assets/9b8e2537-f740-4268-96ec-ab84edeb8b5c" />

- Cercare
   <img width="771" height="552" alt="immagine" src="https://github.com/user-attachments/assets/dfe05e25-1876-43f5-ada3-268b2a22d423" />

  
SE È ANDATO TUTTO CORRETTAMENTE DOVREMMO VEDERLO COSÌ NELLA HOME PAGE DI SERVER MANAGER:
<img width="661" height="519" alt="immagine" src="https://github.com/user-attachments/assets/fa1c250d-c849-4859-9e2d-d4eed4c3c908" />


Per creare un nuovo utente da GUI cerchiamo: 

<img width="356" height="102" alt="immagine" src="https://github.com/user-attachments/assets/29844ec2-df50-4448-bb8b-bbe1da7b3298" />

Click destro e selezioniamo Nuovo> Utente 
Si apre una schermata del genere:

 - <img width="519" height="447" alt="immagine" src="https://github.com/user-attachments/assets/e7b62e81-cac6-4e4d-83f0-69eea7cdb815" />

Impostata una password che **NB** deve contenere caratteri alfanumerici e simboli per esser accettata.
Nel mio caso ho deciso di selezionare di non cambiare la password e non richiedere un cambiamento obbligatorio all'accesso successivo ma come best practice sarebbe meglio abilitare la spunta e lasciare la scadenza

<img width="426" height="369" alt="immagine" src="https://github.com/user-attachments/assets/ccfc5e0c-65ce-4316-8cb1-d0819f373688" />

<img width="432" height="365" alt="immagine" src="https://github.com/user-attachments/assets/a7f02870-102d-4005-9be0-96ad57bbf843" />


Premendo fine avremo il nostro utente: 
- <img width="757" height="527" alt="immagine" src="https://github.com/user-attachments/assets/26a1d865-f518-4007-a110-7ec884f5681a" />

Questa operazione si può eseguire anche su Powershell tramite il comando: New-ADUser compilando poi i vari dati necessari

New-ADUser -Name "Mario Rossi" -GivenName "Mario" -Surname "Rossi" -SamAccountName "m.rossi" -UserPrincipalName "m.rossi@prova.ad" -AccountPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force) `
-Enabled $true

<img width="1012" height="102" alt="immagine" src="https://github.com/user-attachments/assets/6c28548d-6e42-4997-975c-93dc03ad505a" />

Come verifica possiam sempre andare a controllare nella cartella Utenti:

<img width="740" height="515" alt="immagine" src="https://github.com/user-attachments/assets/0599d36d-fa43-43e5-8abc-ff3041b92482" />

