# Chart of Accounts Export

# File Format
Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name: IZPIS GLAVNE KNJIGE.TXT

# Request filters

- Posting Date - mandatory
- G/L Account No.

# Layout

No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV
---|-------------|-----------|------|----------|---------------------------|----------------|-----------------|---------|------------
1|1|10|10|N|G/L account no.|the first 10 characters, left alignment|**Konto**|G/L Account|No.
2|12|61|50|AN|G/L account name|the first 50 characters, left alignment|**Ime konta**|G/L Account|Name
3|63|70|8|N|Posting date|format DDMMLLLL|**Dat knj**|G/L Entry|Posting Date
4|72|79|8|N|Document date|format DDMMLLLL|**Dat lis**|G/L Entry|Document Date
5|81|110|30|AN|Document No.|the first 30 characters, left alignment|**Oznaka listine**|G/L Entry|Document No.
6|112|114|3|AN|Opening (OTV) or closing tag (ZAK) for G/L Entries|OTV, ZAK|**Tip**|G/L Account|OTV - G/L Account Balance on last date of previous fiscal year if Posting Date filter begins on first date of the year. ZAK - G/L Entries posted on Closing date at the end of Posting Date filter
7|116|165|50|AN|Description for G/L transaction|the first 50 characters, left alignment|**Opis**|G/L Entry|Description
8|167|182|16|N|Debit Amount|right alignment, format -999999999999.99|**Breme**|G/L Entry|Debit Amount
9|184|199|16|N|Credit Amount|right alignment, format -999999999999.99|**Dobro**|G/L Entry|Credit Amount
10|201|360|160|AN|Notes - not mandatory|left alignment|**Opombe**|G/L Entry|Entry No.