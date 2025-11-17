![Engineering logo](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Engineering_logo.png/150px-Engineering_logo.png)
autore dei documenti Alberto Pandori

---

# Documentazione Tecnica - Indice

Questa cartella contiene la documentazione tecnica completa dei programmi e delle strutture database del progetto Vorwerk Italia IBM i.

## Repository Sorgente

**Repository:** DevExpPlatform/project-am-vorwerk-italia-ibmi  
**Branch:** out-sync  
**Sistema:** IBM i (AS/400)  

## Documenti Disponibili

### 1. Programmi RPGLE

#### [AGG62230_technical_documentation.md](./AGG62230_technical_documentation.md)
Documentazione tecnica completa del programma AGG62230.

**Contenuto:**
- Informazioni generali e scopo del programma
- Architettura e componenti
- File utilizzati e parametri
- Flusso di elaborazione
- Procedure e sottoprogrammi
- Gestione errori e logging
- Dipendenze e performance
- Testing e deployment

**Path sorgente:** AS4B60MI.EFLTSRC.QRPGLESRC.AGG62230

---

#### [AGG_ALB_V2_technical_documentation.md](./AGG_ALB_V2_technical_documentation.md)
Documentazione tecnica completa del programma AGG_ALB_V2 (Versione 2.0).

**Contenuto:**
- Informazioni generali e scopo del programma
- Novità della versione 2.0
- Architettura e componenti avanzati
- Regole di business e validazioni
- Flusso di elaborazione dettagliato
- Procedure e sottoprogrammi
- Gestione errori multilivello
- Performance e ottimizzazioni
- Configurazione e monitoraggio
- Testing avanzato e troubleshooting

**Path sorgente:** AS4B60MI.EFLTSRC.QRPGLESRC.AGG_ALB_V2

---

### 2. Database

#### [EKLDADBFL_database_documentation.md](./EKLDADBFL_database_documentation.md)
Documentazione completa dello schema database e delle tabelle utilizzate dai programmi.

**Contenuto:**
- Struttura tabelle con DDL completo
- Relazioni e vincoli di integrità referenziale
- Indici e ottimizzazioni
- Trigger e stored procedures
- Views e query di esempio
- Procedure di backup e restore
- Sicurezza e autorizzazioni
- Monitoring e diagnostica
- Migrazione e versioning

**Path sorgente:** AS4B60MI.database.tables.EKLDADBFL

---

## Struttura Documentazione

Ogni documento segue una struttura standardizzata per facilitare la consultazione:

### Per i Programmi:
1. **Informazioni Generali** - Metadata e identificazione
2. **Scopo e Architettura** - Obiettivi e design
3. **Componenti Tecnici** - File, parametri, procedure
4. **Flusso Operativo** - Elaborazione e logica
5. **Gestione Errori** - Error handling e logging
6. **Dipendenze** - Programmi e librerie correlate
7. **Performance** - Metriche e ottimizzazioni
8. **Sicurezza** - Autorizzazioni e protezione dati
9. **Manutenzione** - Storia modifiche e problemi noti
10. **Testing** - Test case e strategie
11. **Deployment** - Installazione e configurazione

### Per il Database:
1. **Struttura Tabelle** - DDL e definizioni complete
2. **Relazioni** - Diagrammi ER e foreign keys
3. **Indici** - Performance e query optimization
4. **Oggetti Procedurali** - Trigger, stored procedures, views
5. **Query di Esempio** - Pattern comuni di utilizzo
6. **Manutenzione** - Backup, restore, reorganizzazione
7. **Sicurezza** - Grant e audit
8. **Monitoring** - Diagnostica e performance tuning

---

## Come Utilizzare la Documentazione

### Per Sviluppatori
- Consultare la documentazione dei programmi per comprendere la logica di business
- Verificare le dipendenze prima di modificare il codice
- Seguire le convenzioni di naming e coding standards
- Aggiornare la documentazione dopo modifiche significative

### Per Database Administrators
- Utilizzare gli script DDL per ricreare strutture
- Consultare le query di esempio per troubleshooting
- Seguire le procedure di backup e manutenzione
- Monitorare le performance utilizzando le query fornite

### Per Team di Test
- Seguire i test case documentati
- Verificare i prerequisiti per ogni scenario
- Utilizzare i codici di errore per validare comportamenti
- Documentare nuovi test case identificati

### Per Operations
- Seguire le procedure di deployment
- Utilizzare le checklist pre e post-deploy
- Consultare la sezione troubleshooting per problemi comuni
- Monitorare le metriche di performance documentate

---

## Standard e Convenzioni

### Naming Conventions

**Programmi:**
- RPGLE programs: Nome descrittivo, max 10 caratteri
- Suffisso `_V2`, `_V3` per versioni successive

**Database:**
- Tabelle: UPPERCASE, nome descrittivo
- Colonne: UPPERCASE con underscore
- Indici: `IDX_[TABELLA]_[CAMPO]`
- Constraint: `[TIPO]_[TABELLA]`

### Versionamento
- Seguire semantic versioning (MAJOR.MINOR.PATCH)
- Documentare ogni cambio di versione nella sezione "Storia delle Modifiche"
- Mantenere backward compatibility quando possibile

---

## Manutenzione della Documentazione

### Responsabilità
- **Sviluppatori:** Aggiornare documentazione con ogni modifica significativa
- **Lead Developer:** Review e approvazione modifiche documentazione
- **Technical Writer:** Coordinamento e standardizzazione

### Processo di Aggiornamento
1. Modificare il documento rilevante nella cartella `docs/`
2. Aggiornare la data di "Ultima revisione"
3. Aggiungere entry nella sezione "Storia delle Modifiche"
4. Sottoporre a review
5. Commit delle modifiche con messaggio descrittivo

### Frequenza Revisione
- **Minima:** Ad ogni release
- **Consigliata:** Mensile per programmi attivi
- **Database:** Ad ogni modifica schema

---

## Risorse Aggiuntive

### Documentazione IBM i
- [IBM i Documentation Center](https://www.ibm.com/docs/en/i)
- [DB2 for i SQL Reference](https://www.ibm.com/docs/en/i/7.4?topic=reference-sql)
- [ILE RPG Reference](https://www.ibm.com/docs/en/i/7.4?topic=languages-ile-rpg)

### Strumenti Consigliati
- **RDi (Rational Developer for i):** IDE per sviluppo RPGLE
- **IBM i Access:** Client access e gestione
- **ACS (Access Client Solutions):** Tools amministrativi moderni

### Contatti Team

**Project Manager:** [Nome]  
**Lead Developer:** [Nome]  
**Database Administrator:** [Nome]  
**Technical Writer:** Alberto Pandori  

---

## Changelog Documentazione

| Data | Versione | Autore | Descrizione |
|------|----------|--------|-------------|
| [Data] | 1.0 | Alberto Pandori | Creazione iniziale documentazione completa |

---

## Note Importanti

⚠️ **Attenzione:**
- Questa documentazione è da considerarsi un template/framework
- Le sezioni marcate con `[placeholder]` devono essere completate con dati reali
- Verificare sempre con i sorgenti effettivi prima di procedere con modifiche
- Mantenere la documentazione sincronizzata con il codice

📝 **Best Practices:**
- Leggere sempre la documentazione prima di modificare codice
- Aggiornare la documentazione immediatamente dopo le modifiche
- Utilizzare esempi concreti e reali
- Mantenere un linguaggio chiaro e tecnico

🔒 **Sicurezza:**
- Non includere password o credenziali nella documentazione
- Marcare sezioni contenenti informazioni sensibili
- Limitare accesso alla documentazione secondo necessità

---

## Licenza e Copyright

**Copyright © [Anno] Engineering Ingegneria Informatica S.p.A.**  
Tutti i diritti riservati.

Questo documento e il suo contenuto sono proprietà di Engineering Ingegneria Informatica S.p.A. e sono da considerarsi confidenziali. La distribuzione, riproduzione o utilizzo non autorizzato è vietato.

---

*Ultima revisione: [Data]*  
*Versione: 1.0*  
*Autore: Alberto Pandori*
