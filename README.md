# Update CSV file with bank entries
An existing file containing entries from different banks, e.g. bank name, BIC, bank code, etc. is updated with [additional entries](https://www.bundesbank.de/resource/blob/602630/2c60c5bacbde19cf9ad0f4910371e982/mL/blz-aktuell-xls-data.xlsx).

## Procedure 
1. Preparing XLSX file with new entries 
2. Update old CSV with new CSV 

### 1. Preparing XLSX file with new entries 
- Removed coloumns that are not needed: Merkmal, PLZ, Ort, Kurzbezeichnung, PAN, Prüfziffer-berechnungs-methode, Datensatz-nummer, Änderungs-kennzeichen, Bankleitzahl-löschung, Nachfolge-Bankleitzahl

### 2. Update old CSV with new CSV 

## Final check
- When converting the file from XLSX to CSV or in the different direction it can happens that Umlaute are converted into replacement characters
- Entries may not be duplicated
