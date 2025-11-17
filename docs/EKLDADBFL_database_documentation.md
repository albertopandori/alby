![Engineering logo](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Engineering_logo.png/150px-Engineering_logo.png)
autore dei documenti Alberto Pandori

---

# Documentazione Database - EKLDADBFL

## Informazioni Generali

**Nome Schema/Libreria:** AS4B60MI.database.tables.EKLDADBFL  
**Repository:** DevExpPlatform/project-am-vorwerk-italia-ibmi  
**Branch:** out-sync  
**Sistema:** IBM i (AS/400)  
**Database:** DB2 for i

## Scopo

Questo documento descrive la struttura delle tabelle database definite in EKLDADBFL, utilizzate dai programmi AGG62230 e AGG_ALB_V2 per la gestione e l'elaborazione dei dati.

## Indice delle Tabelle

1. [Tabella 1 - Nome Tabella](#tabella-1)
2. [Tabella 2 - Nome Tabella](#tabella-2)
3. [Tabella 3 - Nome Tabella](#tabella-3)
4. [Relazioni tra Tabelle](#relazioni)
5. [Indici e Constraint](#indici)

---

## Tabelle Principali

### Tabella 1: [NOME_TABELLA_1]

#### Descrizione
[Descrizione dettagliata dello scopo e utilizzo della tabella]

#### DDL (Data Definition Language)

```sql
CREATE TABLE AS4B60MI.NOME_TABELLA_1 (
    -- Chiave Primaria
    ID_CAMPO1            DECIMAL(10, 0)   NOT NULL,
    
    -- Campi Dati
    CAMPO_DESC1          CHAR(50)         NOT NULL,
    CAMPO_DESC2          VARCHAR(100),
    CAMPO_DATA           DATE,
    CAMPO_TIMESTAMP      TIMESTAMP        DEFAULT CURRENT_TIMESTAMP,
    CAMPO_NUMERICO       DECIMAL(15, 2),
    CAMPO_FLAG           CHAR(1)          DEFAULT 'N',
    
    -- Campi Audit
    CREATED_BY           CHAR(10)         NOT NULL,
    CREATED_DATE         TIMESTAMP        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    UPDATED_BY           CHAR(10),
    UPDATED_DATE         TIMESTAMP,
    
    -- Constraint
    CONSTRAINT PK_TABELLA1 PRIMARY KEY (ID_CAMPO1),
    CONSTRAINT CHK_FLAG CHECK (CAMPO_FLAG IN ('Y', 'N'))
);

-- Label/Descrizioni colonne
LABEL ON COLUMN AS4B60MI.NOME_TABELLA_1.ID_CAMPO1 
    IS 'Identificativo Univoco';
LABEL ON COLUMN AS4B60MI.NOME_TABELLA_1.CAMPO_DESC1 
    IS 'Descrizione Campo 1';

-- Commenti
COMMENT ON TABLE AS4B60MI.NOME_TABELLA_1 
    IS 'Tabella principale per [scopo]';
```

#### Struttura Campi

| Campo | Tipo | Lunghezza | Null | Default | Descrizione |
|-------|------|-----------|------|---------|-------------|
| ID_CAMPO1 | DECIMAL | 10,0 | NO | - | Chiave primaria, identificativo univoco |
| CAMPO_DESC1 | CHAR | 50 | NO | - | Descrizione principale |
| CAMPO_DESC2 | VARCHAR | 100 | YES | NULL | Descrizione secondaria opzionale |
| CAMPO_DATA | DATE | - | YES | NULL | Data riferimento |
| CAMPO_TIMESTAMP | TIMESTAMP | - | YES | CURRENT_TIMESTAMP | Timestamp operazione |
| CAMPO_NUMERICO | DECIMAL | 15,2 | YES | NULL | Valore numerico |
| CAMPO_FLAG | CHAR | 1 | YES | 'N' | Flag Si/No |
| CREATED_BY | CHAR | 10 | NO | - | Utente creazione |
| CREATED_DATE | TIMESTAMP | - | NO | CURRENT_TIMESTAMP | Data creazione |
| UPDATED_BY | CHAR | 10 | YES | NULL | Utente ultima modifica |
| UPDATED_DATE | TIMESTAMP | - | YES | NULL | Data ultima modifica |

#### Indici

```sql
-- Indice primario
CREATE UNIQUE INDEX AS4B60MI.IDX_TAB1_PK 
    ON AS4B60MI.NOME_TABELLA_1 (ID_CAMPO1);

-- Indici secondari
CREATE INDEX AS4B60MI.IDX_TAB1_DESC 
    ON AS4B60MI.NOME_TABELLA_1 (CAMPO_DESC1);

CREATE INDEX AS4B60MI.IDX_TAB1_DATA 
    ON AS4B60MI.NOME_TABELLA_1 (CAMPO_DATA);
```

#### Constraint e Validazioni

| Constraint | Tipo | Descrizione |
|------------|------|-------------|
| PK_TABELLA1 | PRIMARY KEY | Chiave primaria su ID_CAMPO1 |
| CHK_FLAG | CHECK | Verifica che CAMPO_FLAG sia 'Y' o 'N' |

#### Relazioni

- **Foreign Key verso:** [TABELLA_PARENT]
  - Campo: [CAMPO_FK]
  - Descrizione: [Descrizione relazione]

- **Riferita da:** [TABELLA_CHILD]
  - Campo: [CAMPO_FK]
  - Descrizione: [Descrizione relazione]

#### Utilizzo nei Programmi

- **AGG62230:** [Descrizione utilizzo]
- **AGG_ALB_V2:** [Descrizione utilizzo]

---

### Tabella 2: [NOME_TABELLA_2]

#### Descrizione
[Descrizione dettagliata dello scopo e utilizzo della tabella]

#### DDL (Data Definition Language)

```sql
CREATE TABLE AS4B60MI.NOME_TABELLA_2 (
    -- Chiave Primaria Composta
    ID_PRINCIPALE        DECIMAL(10, 0)   NOT NULL,
    ID_SECONDARIO        DECIMAL(10, 0)   NOT NULL,
    
    -- Campi Dati
    CODICE               CHAR(20)         NOT NULL,
    DESCRIZIONE          VARCHAR(200),
    IMPORTO              DECIMAL(15, 2),
    QUANTITA             DECIMAL(10, 3),
    UNITA_MISURA         CHAR(3),
    STATO                CHAR(2)          NOT NULL DEFAULT 'AT',
    DATA_INIZIO          DATE             NOT NULL,
    DATA_FINE            DATE,
    
    -- Campi Tecnici
    VERSION_NUM          INTEGER          NOT NULL DEFAULT 1,
    RECORD_STATUS        CHAR(1)          NOT NULL DEFAULT 'A',
    
    -- Campi Audit
    CREATED_BY           CHAR(10)         NOT NULL,
    CREATED_DATE         TIMESTAMP        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    UPDATED_BY           CHAR(10),
    UPDATED_DATE         TIMESTAMP,
    
    -- Constraint
    CONSTRAINT PK_TABELLA2 PRIMARY KEY (ID_PRINCIPALE, ID_SECONDARIO),
    CONSTRAINT FK_TAB2_TAB1 FOREIGN KEY (ID_PRINCIPALE) 
        REFERENCES AS4B60MI.NOME_TABELLA_1 (ID_CAMPO1)
        ON DELETE CASCADE,
    CONSTRAINT CHK_STATO CHECK (STATO IN ('AT', 'SO', 'CH', 'AN')),
    CONSTRAINT CHK_STATUS CHECK (RECORD_STATUS IN ('A', 'I', 'D')),
    CONSTRAINT CHK_DATE CHECK (DATA_FINE IS NULL OR DATA_FINE >= DATA_INIZIO)
);

-- Commenti
COMMENT ON TABLE AS4B60MI.NOME_TABELLA_2 
    IS 'Tabella dettaglio per [scopo]';
```

#### Struttura Campi

| Campo | Tipo | Lunghezza | Null | Default | Descrizione |
|-------|------|-----------|------|---------|-------------|
| ID_PRINCIPALE | DECIMAL | 10,0 | NO | - | Parte 1 chiave primaria, FK verso TABELLA_1 |
| ID_SECONDARIO | DECIMAL | 10,0 | NO | - | Parte 2 chiave primaria |
| CODICE | CHAR | 20 | NO | - | Codice univoco |
| DESCRIZIONE | VARCHAR | 200 | YES | NULL | Descrizione dettagliata |
| IMPORTO | DECIMAL | 15,2 | YES | NULL | Importo in valuta |
| QUANTITA | DECIMAL | 10,3 | YES | NULL | Quantità |
| UNITA_MISURA | CHAR | 3 | YES | NULL | Unità di misura (KG, LT, PZ, etc) |
| STATO | CHAR | 2 | NO | 'AT' | Stato record (AT=Attivo, SO=Sospeso, CH=Chiuso, AN=Annullato) |
| DATA_INIZIO | DATE | - | NO | - | Data inizio validità |
| DATA_FINE | DATE | - | YES | NULL | Data fine validità |
| VERSION_NUM | INTEGER | - | NO | 1 | Numero versione record (ottimistic locking) |
| RECORD_STATUS | CHAR | 1 | NO | 'A' | Stato record (A=Attivo, I=Inattivo, D=Cancellato logicamente) |
| CREATED_BY | CHAR | 10 | NO | - | Utente creazione |
| CREATED_DATE | TIMESTAMP | - | NO | CURRENT_TIMESTAMP | Data creazione |
| UPDATED_BY | CHAR | 10 | YES | NULL | Utente ultima modifica |
| UPDATED_DATE | TIMESTAMP | - | YES | NULL | Data ultima modifica |

#### Indici

```sql
-- Indice primario
CREATE UNIQUE INDEX AS4B60MI.IDX_TAB2_PK 
    ON AS4B60MI.NOME_TABELLA_2 (ID_PRINCIPALE, ID_SECONDARIO);

-- Indice per FK
CREATE INDEX AS4B60MI.IDX_TAB2_FK1 
    ON AS4B60MI.NOME_TABELLA_2 (ID_PRINCIPALE);

-- Indici per ricerche comuni
CREATE INDEX AS4B60MI.IDX_TAB2_CODICE 
    ON AS4B60MI.NOME_TABELLA_2 (CODICE);

CREATE INDEX AS4B60MI.IDX_TAB2_STATO 
    ON AS4B60MI.NOME_TABELLA_2 (STATO, RECORD_STATUS);

CREATE INDEX AS4B60MI.IDX_TAB2_DATE 
    ON AS4B60MI.NOME_TABELLA_2 (DATA_INIZIO, DATA_FINE);
```

---

### Tabella 3: [NOME_TABELLA_SUPPORTO]

#### Descrizione
Tabella di supporto per [descrizione scopo]

#### DDL (Data Definition Language)

```sql
CREATE TABLE AS4B60MI.NOME_TABELLA_SUPPORTO (
    -- Chiave
    CODICE_TIPO          CHAR(10)         NOT NULL,
    CODICE_VALORE        CHAR(20)         NOT NULL,
    
    -- Dati
    DESCRIZIONE_BREVE    CHAR(50)         NOT NULL,
    DESCRIZIONE_ESTESA   VARCHAR(500),
    VALORE_NUMERICO      DECIMAL(15, 4),
    VALORE_TESTO         VARCHAR(100),
    ORDINAMENTO          INTEGER          DEFAULT 0,
    ATTIVO               CHAR(1)          NOT NULL DEFAULT 'Y',
    
    -- Audit
    CREATED_DATE         TIMESTAMP        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    UPDATED_DATE         TIMESTAMP,
    
    -- Constraint
    CONSTRAINT PK_TABSUPP PRIMARY KEY (CODICE_TIPO, CODICE_VALORE),
    CONSTRAINT CHK_ATTIVO CHECK (ATTIVO IN ('Y', 'N'))
);

-- Commenti
COMMENT ON TABLE AS4B60MI.NOME_TABELLA_SUPPORTO 
    IS 'Tabella di configurazione e parametri';
```

#### Struttura Campi

| Campo | Tipo | Lunghezza | Null | Default | Descrizione |
|-------|------|-----------|------|---------|-------------|
| CODICE_TIPO | CHAR | 10 | NO | - | Tipo parametro/configurazione |
| CODICE_VALORE | CHAR | 20 | NO | - | Valore codice |
| DESCRIZIONE_BREVE | CHAR | 50 | NO | - | Descrizione sintetica |
| DESCRIZIONE_ESTESA | VARCHAR | 500 | YES | NULL | Descrizione dettagliata |
| VALORE_NUMERICO | DECIMAL | 15,4 | YES | NULL | Valore numerico associato |
| VALORE_TESTO | VARCHAR | 100 | YES | NULL | Valore testuale associato |
| ORDINAMENTO | INTEGER | - | YES | 0 | Ordinamento per visualizzazione |
| ATTIVO | CHAR | 1 | NO | 'Y' | Flag attivo/inattivo |
| CREATED_DATE | TIMESTAMP | - | NO | CURRENT_TIMESTAMP | Data creazione |
| UPDATED_DATE | TIMESTAMP | - | YES | NULL | Data ultima modifica |

---

## Relazioni tra Tabelle

### Diagramma ER (Entity-Relationship)

```
┌─────────────────────┐
│  NOME_TABELLA_1     │
│  (Tabella Master)   │
├─────────────────────┤
│ PK: ID_CAMPO1       │
│     CAMPO_DESC1     │
│     ...             │
└──────────┬──────────┘
           │ 1
           │
           │ N
┌──────────▼──────────┐
│  NOME_TABELLA_2     │
│  (Tabella Dettaglio)│
├─────────────────────┤
│ PK: ID_PRINCIPALE   │
│     ID_SECONDARIO   │
│ FK: ID_PRINCIPALE   │
│     CODICE          │
│     ...             │
└─────────────────────┘

┌─────────────────────┐
│ NOME_TABELLA_SUPP   │
│ (Configurazione)    │
├─────────────────────┤
│ PK: CODICE_TIPO     │
│     CODICE_VALORE   │
│     ...             │
└─────────────────────┘
```

### Relazioni Dettagliate

| Tabella Child | Campo FK | Tabella Parent | Campo PK | Tipo | Descrizione |
|---------------|----------|----------------|----------|------|-------------|
| NOME_TABELLA_2 | ID_PRINCIPALE | NOME_TABELLA_1 | ID_CAMPO1 | 1:N | Relazione master-detail |

---

## Indici e Performance

### Indici Principali

| Tabella | Nome Indice | Tipo | Campi | Scopo |
|---------|-------------|------|-------|-------|
| NOME_TABELLA_1 | IDX_TAB1_PK | UNIQUE | ID_CAMPO1 | Chiave primaria |
| NOME_TABELLA_1 | IDX_TAB1_DESC | STANDARD | CAMPO_DESC1 | Ricerca per descrizione |
| NOME_TABELLA_2 | IDX_TAB2_PK | UNIQUE | ID_PRINCIPALE, ID_SECONDARIO | Chiave primaria |
| NOME_TABELLA_2 | IDX_TAB2_FK1 | STANDARD | ID_PRINCIPALE | Performance FK |

### Considerazioni Performance

1. **Partitioning:** Valutare partizionamento per tabelle con alto volume
2. **Statistiche:** Aggiornare statistiche regolarmente con `RUNSTATS`
3. **Indici:** Monitorare utilizzo indici e rimuovere quelli inutilizzati
4. **Archiving:** Implementare strategia archiving per dati storici

---

## Trigger

### Trigger su NOME_TABELLA_1

```sql
-- Trigger per audit automatico
CREATE TRIGGER AS4B60MI.TRG_TAB1_AUDIT
    BEFORE UPDATE ON AS4B60MI.NOME_TABELLA_1
    REFERENCING NEW AS NEW_ROW OLD AS OLD_ROW
    FOR EACH ROW
BEGIN
    SET NEW_ROW.UPDATED_BY = CURRENT_USER;
    SET NEW_ROW.UPDATED_DATE = CURRENT_TIMESTAMP;
END;
```

### Trigger su NOME_TABELLA_2

```sql
-- Trigger per versioning
CREATE TRIGGER AS4B60MI.TRG_TAB2_VERSION
    BEFORE UPDATE ON AS4B60MI.NOME_TABELLA_2
    REFERENCING NEW AS NEW_ROW OLD AS OLD_ROW
    FOR EACH ROW
BEGIN
    SET NEW_ROW.VERSION_NUM = OLD_ROW.VERSION_NUM + 1;
    SET NEW_ROW.UPDATED_BY = CURRENT_USER;
    SET NEW_ROW.UPDATED_DATE = CURRENT_TIMESTAMP;
END;
```

---

## Stored Procedures

### Procedura: SP_INSERT_MASTER_DETAIL

```sql
CREATE PROCEDURE AS4B60MI.SP_INSERT_MASTER_DETAIL(
    IN P_CAMPO_DESC1 CHAR(50),
    IN P_CODICE CHAR(20),
    IN P_IMPORTO DECIMAL(15,2),
    OUT P_ID_NUOVO DECIMAL(10,0),
    OUT P_RESULT_CODE INTEGER,
    OUT P_RESULT_MSG VARCHAR(200)
)
LANGUAGE SQL
BEGIN
    DECLARE V_ID_PRINCIPALE DECIMAL(10,0);
    DECLARE V_ID_SECONDARIO DECIMAL(10,0);
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    BEGIN
        SET P_RESULT_CODE = -1;
        SET P_RESULT_MSG = 'Errore durante inserimento';
        ROLLBACK;
    END;
    
    -- Genera nuovo ID
    SELECT COALESCE(MAX(ID_CAMPO1), 0) + 1 
    INTO V_ID_PRINCIPALE
    FROM AS4B60MI.NOME_TABELLA_1;
    
    -- Insert master
    INSERT INTO AS4B60MI.NOME_TABELLA_1 
        (ID_CAMPO1, CAMPO_DESC1, CREATED_BY)
    VALUES 
        (V_ID_PRINCIPALE, P_CAMPO_DESC1, CURRENT_USER);
    
    -- Insert detail
    INSERT INTO AS4B60MI.NOME_TABELLA_2
        (ID_PRINCIPALE, ID_SECONDARIO, CODICE, IMPORTO, 
         STATO, DATA_INIZIO, CREATED_BY)
    VALUES
        (V_ID_PRINCIPALE, 1, P_CODICE, P_IMPORTO,
         'AT', CURRENT_DATE, CURRENT_USER);
    
    SET P_ID_NUOVO = V_ID_PRINCIPALE;
    SET P_RESULT_CODE = 0;
    SET P_RESULT_MSG = 'Inserimento completato con successo';
    COMMIT;
END;
```

---

## Views

### View: VW_MASTER_DETAIL_COMPLETO

```sql
CREATE VIEW AS4B60MI.VW_MASTER_DETAIL_COMPLETO AS
SELECT 
    T1.ID_CAMPO1,
    T1.CAMPO_DESC1,
    T1.CAMPO_DESC2,
    T2.ID_SECONDARIO,
    T2.CODICE,
    T2.DESCRIZIONE,
    T2.IMPORTO,
    T2.QUANTITA,
    T2.UNITA_MISURA,
    T2.STATO,
    T2.DATA_INIZIO,
    T2.DATA_FINE,
    T1.CREATED_DATE AS MASTER_CREATED_DATE,
    T2.CREATED_DATE AS DETAIL_CREATED_DATE
FROM 
    AS4B60MI.NOME_TABELLA_1 T1
    LEFT JOIN AS4B60MI.NOME_TABELLA_2 T2
        ON T1.ID_CAMPO1 = T2.ID_PRINCIPALE
WHERE 
    T2.RECORD_STATUS = 'A';

-- Commento
COMMENT ON VIEW AS4B60MI.VW_MASTER_DETAIL_COMPLETO 
    IS 'Vista completa master-detail per reporting';
```

---

## Query di Esempio

### Query 1: Estrazione Dati Attivi

```sql
-- Estrai tutti i record attivi con dettagli
SELECT 
    M.ID_CAMPO1,
    M.CAMPO_DESC1,
    D.CODICE,
    D.IMPORTO,
    D.STATO
FROM 
    AS4B60MI.NOME_TABELLA_1 M
    INNER JOIN AS4B60MI.NOME_TABELLA_2 D
        ON M.ID_CAMPO1 = D.ID_PRINCIPALE
WHERE 
    D.STATO = 'AT'
    AND D.RECORD_STATUS = 'A'
    AND (D.DATA_FINE IS NULL OR D.DATA_FINE >= CURRENT_DATE)
ORDER BY 
    M.CAMPO_DESC1, D.CODICE;
```

### Query 2: Aggregazione Importi

```sql
-- Calcola totale importi per master
SELECT 
    M.ID_CAMPO1,
    M.CAMPO_DESC1,
    COUNT(D.ID_SECONDARIO) AS NUM_DETTAGLI,
    SUM(D.IMPORTO) AS TOTALE_IMPORTI,
    AVG(D.IMPORTO) AS MEDIA_IMPORTI
FROM 
    AS4B60MI.NOME_TABELLA_1 M
    LEFT JOIN AS4B60MI.NOME_TABELLA_2 D
        ON M.ID_CAMPO1 = D.ID_PRINCIPALE
        AND D.RECORD_STATUS = 'A'
GROUP BY 
    M.ID_CAMPO1,
    M.CAMPO_DESC1
HAVING 
    COUNT(D.ID_SECONDARIO) > 0
ORDER BY 
    TOTALE_IMPORTI DESC;
```

### Query 3: Ricerca con Parametri

```sql
-- Ricerca parametrizzata
SELECT 
    T.*,
    S.DESCRIZIONE_BREVE AS STATO_DESC
FROM 
    AS4B60MI.NOME_TABELLA_2 T
    LEFT JOIN AS4B60MI.NOME_TABELLA_SUPPORTO S
        ON S.CODICE_TIPO = 'STATO'
        AND S.CODICE_VALORE = T.STATO
WHERE 
    T.DATA_INIZIO BETWEEN ? AND ?
    AND T.IMPORTO >= ?
    AND T.STATO IN (?, ?)
ORDER BY 
    T.DATA_INIZIO DESC;
```

---

## Manutenzione Database

### Backup

```bash
# Backup completo schema
SAVLIB LIB(AS4B60MI) DEV(*SAVF) SAVF(BACKUP/AS4B60MI_YYYYMMDD)

# Backup singola tabella
CPYTOIMPF FROMFILE(AS4B60MI/NOME_TABELLA_1) +
          TOFILE('/backup/nome_tabella_1_yyyymmdd.csv') +
          MBROPT(*REPLACE) STMFCODPAG(*PCASCII)
```

### Restore

```bash
# Restore completo schema
RSTLIB SAVLIB(AS4B60MI) DEV(*SAVF) SAVF(BACKUP/AS4B60MI_YYYYMMDD)
```

### Reorganizzazione

```sql
-- Reorganizza tabella per migliorare performance
CALL QSYS2.ADMIN_REORGANIZE_TABLE('AS4B60MI', 'NOME_TABELLA_1');

-- Aggiorna statistiche
CALL QSYS2.ADMIN_MAINTAIN_INDEXES(
    'AS4B60MI', 
    'NOME_TABELLA_1', 
    'REBUILD'
);
```

### Pulizia Dati Obsoleti

```sql
-- Archivia e rimuovi dati vecchi
BEGIN
    -- Archivia in tabella storico
    INSERT INTO AS4B60MI.NOME_TABELLA_2_STORICO
    SELECT * FROM AS4B60MI.NOME_TABELLA_2
    WHERE DATA_FINE < CURRENT_DATE - 365 DAYS;
    
    -- Cancellazione logica
    UPDATE AS4B60MI.NOME_TABELLA_2
    SET RECORD_STATUS = 'D'
    WHERE DATA_FINE < CURRENT_DATE - 365 DAYS;
    
    COMMIT;
END;
```

---

## Sicurezza e Autorizzazioni

### Grant Necessari per Programmi

```sql
-- Autorizzazioni per programma AGG62230
GRANT SELECT, INSERT, UPDATE ON AS4B60MI.NOME_TABELLA_1 TO AGG62230;
GRANT SELECT, INSERT, UPDATE ON AS4B60MI.NOME_TABELLA_2 TO AGG62230;
GRANT SELECT ON AS4B60MI.NOME_TABELLA_SUPPORTO TO AGG62230;

-- Autorizzazioni per programma AGG_ALB_V2
GRANT SELECT, INSERT, UPDATE, DELETE ON AS4B60MI.NOME_TABELLA_1 TO AGG_ALB_V2;
GRANT SELECT, INSERT, UPDATE, DELETE ON AS4B60MI.NOME_TABELLA_2 TO AGG_ALB_V2;
GRANT SELECT ON AS4B60MI.NOME_TABELLA_SUPPORTO TO AGG_ALB_V2;

-- Autorizzazioni per stored procedures
GRANT EXECUTE ON PROCEDURE AS4B60MI.SP_INSERT_MASTER_DETAIL TO PUBLIC;
```

### Audit Security

```sql
-- Enable auditing
CALL QSYS2.QCMDEXC('CHGOBJAUD OBJ(AS4B60MI/NOME_TABELLA_1) OBJTYPE(*FILE) OBJAUD(*ALL)');
```

---

## Monitoring e Diagnostica

### Query per Monitoraggio

```sql
-- Dimensione tabelle
SELECT 
    TABLE_NAME,
    TABLE_SCHEMA,
    NUMBER_ROWS,
    AVERAGE_ROW_SIZE,
    (NUMBER_ROWS * AVERAGE_ROW_SIZE) / 1024 / 1024 AS SIZE_MB
FROM 
    QSYS2.SYSTABLESTAT
WHERE 
    TABLE_SCHEMA = 'AS4B60MI'
ORDER BY 
    SIZE_MB DESC;

-- Indici non utilizzati
SELECT 
    INDEX_NAME,
    TABLE_NAME,
    LAST_USED_TIMESTAMP,
    DAYS_USED_COUNT
FROM 
    QSYS2.SYSINDEXSTAT
WHERE 
    TABLE_SCHEMA = 'AS4B60MI'
    AND LAST_USED_TIMESTAMP < CURRENT_TIMESTAMP - 90 DAYS
ORDER BY 
    LAST_USED_TIMESTAMP;
```

---

## Migrazione e Versioning

### Script Migrazione Schema

```sql
-- Versione 1.0 -> 1.1
-- Aggiunta colonna EMAIL a NOME_TABELLA_1
ALTER TABLE AS4B60MI.NOME_TABELLA_1 
ADD COLUMN EMAIL VARCHAR(100);

-- Aggiorna versione schema
INSERT INTO AS4B60MI.SCHEMA_VERSION 
    (VERSION, APPLIED_DATE, DESCRIPTION)
VALUES 
    ('1.1', CURRENT_TIMESTAMP, 'Aggiunta colonna EMAIL');
```

---

## Contatti e Riferimenti

**Autore:** Alberto Pandori  
**Database Administrator:** [Nome DBA]  
**Team:** [Nome team]  

### Documentazione Correlata
- [Link a documentazione programmi AGG62230]
- [Link a documentazione programmi AGG_ALB_V2]
- [Link a standard naming conventions]

### Risorse Utili
- IBM i Documentation: [link]
- DB2 for i SQL Reference: [link]

---

## Appendice: Convenzioni di Naming

### Tabelle
- Nomi in UPPERCASE
- Prefisso per tipo tabella se applicabile
- Nomi descrittivi del contenuto

### Colonne
- Nomi in UPPERCASE con underscore per separazione
- Suffissi standard:
  - `_ID` per identificativi
  - `_DATE` per date
  - `_FLAG` per flag Y/N
  - `_BY` per utenti
  - `_NUM` per contatori/numeri

### Indici
- Formato: `IDX_[TABELLA]_[CAMPO/I]`
- Suffisso `_PK` per primary key
- Suffisso `_FK` per foreign key

### Constraint
- Formato: `[TIPO]_[TABELLA]`
- Tipi: PK (Primary Key), FK (Foreign Key), CHK (Check), UQ (Unique)

---

## Note Finali

Questa documentazione è da considerarsi un template e deve essere completata con i dettagli specifici delle tabelle effettivamente presenti in EKLDADBFL.

Per informazioni aggiuntive o chiarimenti, contattare il team di sviluppo.

---

*Documento generato il: [Data]*  
*Ultima revisione: [Data]*  
*Versione documento: 1.0*
