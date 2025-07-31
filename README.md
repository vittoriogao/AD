# Guida: Configurare Active Directory su Windows Server 2025

Benvenuto in questa guida passo passo su come installare e configurare Active Directory.

Il mio approccio scelto è stato tramite **PowerShell**, uno strumento più potente e rapido rispetto alla interfaccia grafica (GUI).

## Metodo 1: Installazione tramite PowerShell (Consigliato)

Questo metodo è il più veloce

### Passaggio 1: Installare il Ruolo Active Directory

  Collegati alla tua macchina Windows Server 2025. Apri una finestra di **PowerShell con privilegi di amministratore**.
   Lancia il seguente comando per installare i servizi di dominio e gli strumenti di gestione:

    Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
    ```
    Al termine, vedrai un output simile a questo, che conferma il successo dell'operazione:
    
    (https://github.com/user-attachments/assets/bb432684-6745-49d8-9219-99c4419e6e77)

 Ora lancia il comando per creare la nuova foresta. **Sostituisci i valori di esempio** con quelli desiderati.

    ```powershell
    Install-ADDSForest `
        -DomainName "esempio" `
        -DomainNetbiosName "qua potrai cambiarlo in un nome più breve" `
        -InstallDns:$true `
        -ForestMode Win2025 `
        -DomainMode Win2025 `
        -SafeModeAdministratorPassword ( `
        -Force
    ```

> **Nota:** Dopo aver eseguito l'ultimo comando, il server verrà **riavviato** per completare la configurazione.

---

## Metodo 2: Installazione tramite Interfaccia Grafica (GUI)


- Se volessimo invece farlo da GUI:
   - tasto Start e cerchiamo Server Manager
  - Successivamente Aggiungi ruoli e funzionalità
   (https://github.com/user-attachments/assets/360487e7-3453-460c-940d-d1ca2ae4cfe)

- Premere avanti (Next)
(https://github.com/user-attachments/assets/ae0eadd4-5ac1-42f9-8e78-b947421a66c5)

   -Selezionare Role-based or feature-based installation.

 (https://github.com/user-attachments/assets/dc5d0a48-638b-4b39-9cc9-7559124dee46)


  
SE È ANDATO TUTTO CORRETTAMENTE DOVREMMO VEDERLO COSÌ:
<img width="661" height="519" alt="immagine" src="https://github.com/user-attachments/assets/a13f39b8-1dce-4229-bbfa-5bd53ea1bec1" />


Per creare un nuovo utente da GUI cerchiamo: 

  <img width="356" height="102" alt="immagine" src="https://github.com/user-attachments/assets/51ad40f2-dc37-4654-a832-7fb4ffd6b997" />

Click destro e selezioniamo Nuovo> Utente 

- <img width="519" height="447" alt="immagine" src="https://github.com/user-attachments/assets/bab81d00-e48d-4333-a12c-8b204a2f1ac7" />

Si apre una schermata del genere:

 - <img width="425" height="364" alt="immagine" src="https://github.com/user-attachments/assets/7c596bc6-3c64-4cfb-bf56-484cc683db3d" />


Impostata una password che **NB** deve contenere caratteri alfanumerici e simboli per esser accettata.
Nel mio caso ho deciso di selezionare di non cambiare la password e non richiedere un cambiamento obbligatorio all'accesso successivo ma come best practice sarebbe meglio abilitare la spunta e lasciare la scadenza

- <img width="432" height="365" alt="immagine" src="https://github.com/user-attachments/assets/9459394f-2c63-4af2-a4f3-7033467438c4" />

Premendo fine avremo il nostro utente: 
- <img width="757" height="527" alt="immagine" src="https://github.com/user-attachments/assets/88838014-46f8-48c4-bfeb-6be9a9a91f39" />

Questa operazione si può eseguire anche su Powershell tramite il comando: New-ADUser compilando poi i vari dati necessari

New-ADUser -Name "Mario Rossi" -GivenName "Mario" -Surname "Rossi" -SamAccountName "m.rossi" -UserPrincipalName "m.rossi@prova.ad" -AccountPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force) `
-Enabled $true

<img width="1012" height="102" alt="immagine" src="https://github.com/user-attachments/assets/f5aa6103-b82b-4927-80c4-f12c75799c68" />

Come verifica possiam sempre andare a controllare nella cartella Utenti:

<img width="740" height="515" alt="immagine" src="https://github.com/user-attachments/assets/67570a62-2046-437f-a6fa-e32a2d2c7be8" />

