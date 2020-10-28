# Update CSV file with bank entries
An existing file containing entries from different banks, e.g. bank name, BIC, bank code, etc. is updated with [additional entries](https://www.bundesbank.de/resource/blob/602630/2c60c5bacbde19cf9ad0f4910371e982/mL/blz-aktuell-xls-data.xlsx).

<br>

## Prerequisite

- install Python
- you can use jupyter notebook for executing the files (recommended):
   - install jupyter with brew, conda or pip: `brew install jupyter`
   - start jupyter notebook on Mac: `jupyter notebook`

## Procedure 
In the following the Bundesbank file is the base file, which must be adapted to the given structure:

1. Preparing file from the Bundesbank
2. Check for redundant entries
3. Add data to Adapter Id and productive URL

<br>

### 1. Preparing file from the Bundesbank
#### Create same structure like existing CSV 
1. **Remove columns that are not needed:** Merkmal, PLZ, Ort, Kurzbezeichnung, PAN, Prüfziffer-berechnungs-methode, Datensatz-nummer, Änderungs-kennzeichen, Bankleitzahl-löschung, Nachfolge-Bankleitzahl
2. **Create the following column order:** Id, Bank Name, BIC, URL, Adapter Id, Bank Code, IDP URL, Approach (Bank Name and Bank Code should be already filled up, BIC partly)
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

### 3. Add data to AdapterId and productive URL

#### Add AdapterId and URL
By using [**addURLandAdapterId.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/addURLandAdapterId.ipynb) data for the common banks will be added

*Check how many and which entries are still empty:*
After using [**addURLandAdapterId.ipynb**](https://github.com/VeronikaSedlackova/UpdateCSV_BankEntries/blob/master/addURLandAdapterId.ipynb) the information will be displayed in the last command output


#### Remaining columns
*Id:* Will be added by the ASPSP Registry Manager

*IDP URL, Approach:* will propably remain empty

<br> 

## Final check
- When converting the file from XLSX to CSV or in the different direction it can happens that Umlaute are converted into replacement characters
