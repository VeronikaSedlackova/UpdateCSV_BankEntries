# Update CSV file with bank entries
An existing file containing entries from different banks, e.g. bank name, BIC, bank code, etc. is updated with [additional entries](https://www.bundesbank.de/resource/blob/602630/2c60c5bacbde19cf9ad0f4910371e982/mL/blz-aktuell-xls-data.xlsx).

## Procedure 
In the following the Bundesbank file is the base file, which must be adapted to the given structure:

1. Preparing file from the Bundesbank
2. Check for redundant entries
3. Add data for Adapter Id and productive URL
4. Check if there are missing entries from the old in the new CSV | ASK: wenn Eintrag in alt veraltet ist (zb wegen Fusion) und ich auf difference prüfe kommt die wieder in die neue Datei

### 1. Preparing file from the Bundesbank
#### Create same structure like existing CSV 
1. **Remove columns that are not needed:** Merkmal, PLZ, Ort, Kurzbezeichnung, PAN, Prüfziffer-berechnungs-methode, Datensatz-nummer, Änderungs-kennzeichen, Bankleitzahl-löschung, Nachfolge-Bankleitzahl
2. **Create the following column order:** Id, Bank Name, BIC, URL, Adapter Id, Bank Code, IDP URL, Approach (Bank Name and Bank Code should be already filled up, BIC partly)
3. **Convert to CSV:** You can use [Convertio](https://convertio.co/de/)
4. **Delete all quotes if present:** use removeQuotes.ipynb

### 2. Check for redundant entries
There are entries for the same bank that are redundant. That means, if the bank's bank code is the same and at the same time the BIC is empty except for one entry or alle BIC's are equal, all these entries except for one must be removed. 

*An entry is not redundant for a bank if:*
- Bank Code and BIC are different
- Bank Code ist the same but BIC is always different

### 3. Add data for Adapter Id and productive URL

#### Add Adapter Id
Has to the filled up manually

#### Add URL
Has to the filled up manually

#### Remaining columns
*Id:* Will be added by the ASPSP Registry Manager

*IDP URL, Approach:* will propably remain empty


## Final check
- When converting the file from XLSX to CSV or in the different direction it can happens that Umlaute are converted into replacement characters
- Entries may not be duplicated

## Open questions
alte Datei sortieren nach Bankname damit durchlaufzeit fuer jede Bank nicht so hoch? --> testen ob ohne Sortierung möglich (sonst fragen ob alte Datei sortiert werden darf)
