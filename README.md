# Update CSV file with bank entries
A [file](https://www.bundesbank.de/dynamic/action/de/startseite/suche/747716/allgemeine-suche?query=unicredit) from *Deutsche Bundesbank* contains specific bank information and has to be adapted to certain requirements.

<br>

## Prerequisite

- install Python
- you can use jupyter notebook for executing the files (recommended):
   - install jupyter with brew, conda or pip: `brew install jupyter`
   - start jupyter notebook on Mac: `jupyter notebook`
   
- download [previous CSV file](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/aspsp-adapter-config.csv) 

## Procedure 
The Bundesbank file is the base file, which must be adapted in the following order:

1. Preparing file from the Bundesbank
2. Check for redundant entries
3. Add data
<br>

### 1. Preparing file from the Bundesbank
#### Create same structure like existing CSV 
1. **Remove columns that are not needed:** Merkmal, PLZ, Ort, Kurzbezeichnung, PAN, Prüfziffer-berechnungs-methode, Datensatz-nummer, Änderungs-kennzeichen, Bankleitzahl-löschung, Nachfolge-Bankleitzahl
2. **Create the following column order:** Id, Bank Name, BIC, URL, Adapter Id, Bank Code (=Bank-leitzahl), IDP URL, Approach (Bank Name and Bank Code should be already filled up, BIC partly)
3. **Sometimes there is an comma in the bank name. It has to be removed! You can do it in Excel:**

   - Select the whole column "Bank Name"
   - Go to "search and select" and then click on "replace"
   - Enter a comma to "search for" and leave the "replace" input empty
   - Click on "replace all"
  
   Check if it worked:
   - Put a filter over the column description
   - Look if there is still a comma in the option "contains"

4. **Sort the bank name in ascending order**
5. **Convert to CSV:** You can use [Convertio](https://convertio.co/de/)
6. **Delete all quotes if present:** use [**removeQuotes.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/removeQuotes.ipynb)
7. **Make sure that the initial column description: *Id, Bank Name, BIC, URL, Adapter Id, Bank Code, IDP URL, Approach* is deleted**

<br>

### 2. Check for redundant entries
There are entries for the same bank that are redundant. 

*Entries that have to be removed:*
- Bank codes are equal and at the same time the BIC is empty except for one entry -> delete all entries without the BIC 
- Bank codes are equal, BICs are equal

*An entry is not redundant for a bank if:*
- Bank code and BIC are different
- Bank code is the same but BIC is always different
- Bank code is different to all bank codes (of the same bank) AND no BIC is present

Use [**removeRedundancy.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/removeRedundancy.ipynb) to remove redundant rows

<br>

### 3. Add data 

#### Add AdapterId, productive URL and partly IDP URL
By using [**addData.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/addData.ipynb) data for the common banks will be added

- *Check how many and which entries are still empty:*
After using **addData.ipynb** the information will be displayed in the last command output

- *If too many entries are still empty you can use an extended file which adds data to selected banks:* [**addData_extended.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/addData_extended.ipynb)


#### Remaining columns
*Id:* Will be added by the ASPSP Registry Manager

*IDP URL, Approach:* will propably remain empty

<br>

## Final check/information
- When converting the file from XLSX to CSV or in the different direction it can happens that umlaute are converted into replacement characters. You can use [this file](https://github.com/VeronikaSedlackova/Converter-for-wrong-formatted-Umlaute) to get back the right umlaute
- <h4>The resulting file is called: addedData_final.csv</h4>

