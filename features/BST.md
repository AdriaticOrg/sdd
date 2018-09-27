# BST Report

BST Report enables reporting of services and part of goods exchange and current/capital transfers with non-residents to Bank of Slovenia (BSI) on monthly basis grouped by BST codes and Countries/Regions Codes. Report is submitted through xml data file.

> Range: 13.062.681..13.062.700

> Country: SI
## Scope

User must be able to setup the necessary data for BST reporting and print the report which also has the option to export data to xml file. In general, besides BST Setup, setup process includes filling two additional fields: BST Code-Adl and BST Value Posting-Adl on G/L Account records. Prior to this action, BST Code records should be inserted.

## Architectural Design

BST Code-Adl is added to G/L Account master table. During any financial posting which results in a General Ledger Entry, value in this field is populated with value from G/L Account if available. On G/L Account we have one additional field:
> BST Value Posting-Adl: indicates on which side of BST report (Debit, Credit) values should be included.

Additionally we need to populate Country/Region Code in Gen. Journal Line in case of validating Account No. or Bal. Account No. with Customer or Vendor. In this case we copy value from there, to make sure, Country/Region Code will be available for BST Report creation.
> 
## Data Design

Fields BST Code-Adl, BST Value Posting-Adl are added to table 15 G/L Account.

Fields BST Code is added also to 17 G/L Entry table.

New objects are:

Type|Name
--|----|
Table Extension|BST Code-Adl
Table Extension|Gen. Journal Line-Adl
<br>|<br>
Page Extension|G/L Account Card-Adl
Page Extension|General Ledger Entries-Adl
<br>|<br>
Table|BST Setup-Adl
Table|BST Code-Adl
Table|BST Report Header-Adl
Table|BST Report Line-Adl
<br>|<br>
Page|BST Setup-Adl
Page|BST Codes-Adl
Page|BST Reports-Adl
Page|BST Report-Adl
Page|BST Report Subform-Adl
<br>|<br>
Report|Suggest BST Lines-Adl
Report|Export BST-Adl

## Data Flow

Process Name|Scope
--|--
Journal validation|When entering Customer/Vendor in Account No. and Bal. Account No. in General Journal Line, populate Country/Region Code from master table.
Gen. Journal Line posting|Transfer BST Code-Adl from G/L Account to G/L Entry.|
Report preparing|Open new Reporting document for the period in question, run the suggest lines process to populate Reporting document lines. Manually adjust lines if needed. Run the Export BST activity to get the hard copy and/or xml file saved to disk.|

## User Interface

New BST related filedls should be visible on relevant page extensions for viewing and/or editing.

>Note: this file may be subject of change in near future if need arises.
