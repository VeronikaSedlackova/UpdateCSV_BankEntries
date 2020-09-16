# Update CSV file with bank entries
An existing file containing entries from different banks, e.g. bank name, BIC, bank code, etc. is updated with [additional entries](https://www.bundesbank.de/resource/blob/602630/2c60c5bacbde19cf9ad0f4910371e982/mL/blz-aktuell-xls-data.xlsx).

## Procedure 
1. Preparing XLSX file with new entries 
2. Update old CSV with new CSV 

### 1. Preparing file from the Bundesbank
#### Create same structure like existing CSV 
1. **Remove columns that are not needed:** Merkmal, PLZ, Ort, Kurzbezeichnung, PAN, Prüfziffer-berechnungs-methode, Datensatz-nummer, Änderungs-kennzeichen, Bankleitzahl-löschung, Nachfolge-Bankleitzahl
2. **Create the following column order:** Id, Bank Name, BIC, URL, Adapter Id, Bank Code, IDP URL, Approach 
  
  `Id: Will be added by the ASPSP Registry Manager`
  
  `URL: Has to the filled up manually`
  
  `Adapter Id: Has to the filled up manually`
  
  `IDP URL, Approach: will propably remain empty`
  
3. **Sort the bank name in ascending order**
4. **Add data of Bank Name, BIC and Bank Code to the corresponding columns**
5. **Convert to CSV:** You can use [Convertio](https://convertio.co/de/)
6. **Delete all quotes if present** TODO

#### Add URL

#### Add Adapter Id


### 2. Update old CSV with new CSV 

## Final check
- When converting the file from XLSX to CSV or in the different direction it can happens that Umlaute are converted into replacement characters
- Entries may not be duplicated

## Open questions
alte Datei sortieren nach Bankname damit durchlaufzeit fuer jede Bank nicht so hoch? --> testen ob ohne Sortierung möglich (sonst fragen ob alte Datei sortiert werden darf)
