# Export GL and VAT Ledgers for Tax Authorities SI

## Feature requirement

Export GL and VAT Ledgers on Tax Authorities demand functionality enables exporting of Electronic VAT books and G/L ledgers in format prescribed by Tax authorities.

## New Required Objects

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Codeunit Extension|New Object|CUxxxxGLEntryExportSI -ADL
2.|Codeunit Extension|New Object|CUxxxxInputVATBookExportSI -ADL
3.|Codeunit Extension|New Object|CUxxxxOutputVATBookExportSI -ADL
  
-----
-----
       
**1. GL Entry Export - SI:**

Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name - IZPIS GLAVNE KNJIGE.TXT

Export filters:
 - Posting Date - mandatory
 - G/L Account No.


No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV
--|---|---|---|---|-----------------|----|-----------|-----|----
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

--------
--------

**2. Input VAT Book Export - SI:**

Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name - IZPIS ODBITKA DDV.TXT

Export VAT Entries where Amount or/and Base are not null. 

Export filters:
 - Posting Date - mandatory
 - Document No.

 No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV|VAT Identifier filter|Type
--|--|--|--|------|-------|--------|----|-----|----|----|----|----
1|1|4|4|N|VAT periodPosting Date in format <Month,2><Month,2>|**Odb**|VAT Entry|Posting Date
2|6|13|8|N|Posting date|format DDMMLLLL|**Dat knj**|VAT Entry|Posting Date
3|15|22|8|N|OutputPosting Date|format DDMMLLLL|**Dat pre**|VAT Entry|Document Receipt Date
4|24|53|30|AN|Document No.|the first 30 characters, left alignment|**Številka listine**|VAT Entry|Document No.
5|55|62|8|N|Document date|format DDMMLLLL|**Dat lis**|VAT Entry|Document Date
6|64|113|50|AN|Vendor name and address|the first 50 characters, left alignment|**Dobavitelj**|Posted document /Vendor /Customer|Pay-to Name, Pay-to Address, Pay-to City, Pay-to Country/Region Code
7|115|134|20|AN|Vendor VAT registration No.|the first 20 characters, left alignment|**IŠ za DDV**|VAT Entry|VAT Registration No.
8|136|151|16|N|The value of purchases of goods and services excluding VAT|right alignment, format -999999999999.99|**Vred brez DDV**|VAT Entry|Base|10, 11, 12, 13, 23, 111, 112, 4010, 4011, 4012, 4013, 4023, 4026, 4111, 4112, 5010, 5011, 5012, 5111, 5112, 29, 20, 30, 4020, 5020|Type: Purchase
|||||||||||18, 6023, 25, 26, 107, 108, 4108, 27, 6013, 4623, 4613, 6053, 6063, 4653, 4663|Type: Sale
9|153|168|16|N|The value of purchases of goods and services in Slovenia from reverse charge VAT|right alignment, format -999999999999.99|**Vred SAMOOBD**|VAT Entry|Base|5141, 5140, 5041, 5040, 41, 40, 141, 140, 42, 43, 5042, 5043, 5142, 5143, 142, 143, 4042, 4043, 4142, 4143, 44, 5044, 4041, 4040|Type: Sale
10|170|185|16|N|The value of purchases of goods from EU|right alignment, format -999999999999.99|**Vred PRID BLA**|VAT Entry|Base|130|Type: Purchase
|||||||||||311, 312, 313, 314, 4311, 4312, 4313, 4314, 5313, 317, 318, 5314| Type: Sale
11|187|202|16|N|The value of purchases of services from EU|right alignment, format -999999999999.99|**Vred PREJ STOR**|VAT Entry|Base|15, 16, 5016, 4016, 110, 109, 4110, 28| Type: Sale
12|204|219|16|N|The value of purchases of real estates excluding VAT|right alignment, format -999999999999.99|**Vred OBD NEPR**|VAT Entry|Base|5010, 5011, 5012, 5111, 5112, 5020|Type: Purchase
|||||||||||5313, 5314, 5016, 5141, 5140, 5041, 5040, 5042, 5043, 5142, 5143, 5044|Type: Sale
13|221|236|16|N|The value of purchases of fixed assets excluding VAT|right alignment, format -999999999999.99|**Vred OBD OS**|VAT Entry|Base|4010, 4011, 4012, 4013, 4023, 4026, 4111, 4112, 4020, 4653, 4663|Type: Purchase
|||||||||||4313, 4314, 4311, 4312, 4016, 4108, 4110, 4042, 4043, 4143, 4041, 4040, 4623, 4613| Type: Sale 
14|238|253|16|N|The value of exempt purchases and purchases in EU excluding VAT|right alignment, format -999999999999.99|**Vrednost ON**|VAT Entry|Base|8, 309, 4008, 4309, 5008|Type: Purchase
15|255|270|16|N|The value of exempt purchases of of real estates excluding VAT|right alignment, format -999999999999.99|**Vred OPR NEPR**|VAT Entry|Base|5008|Type: Purchase
16|272|287|16|N|The value of exempt purchases of of fixed assets excluding VAT|right alignment, format -999999999999.99|**Vred OPR OS**|VAT Entry|Base|4008, 4309|Type: Purchase
17|289|304|16|N|Undeductable VAT|right alignment, format -999999999999.99|**Neodbitni DDV**|VAT Entry|VAT Amount|10, 4010, 5010, 311, 312, 4311, 4312, 110, 107, 108, 109, 42, 43, 5042, 5043, 5142, 5143, 142, 143, 4108, 4110, 20, 4020, 5020, 4042, 4043, 4143, 11, 12, 5011, 5012, 4011, 4012, 29, 991, 992, 11, 5041, 5040, 41, 40, 4041, 4040, 4023, 4026, 23, 13, 314, 313, 5016, 4314, 4313, 4016, 16, 15, 4108, 26, 25, 5314, 6053, 6063, 4653, 4663|Type: Purchase
18|306|321|16|N|Deductable VAT 22%|right alignment, format -999999999999.99|**VST 22% DDV**|VAT Entry|VAT Amount|16, 314, 4314, 5314, 6023, 5016, 4016, 5141, 5041, 41, 141, 26, 12, 23, 112, 5012, 4012, 4023, 4026, 4112, 5112, 4041, 4623|Type: Purchase
19|323|338|16|N|Deductable VAT 9,5%|right alignment, format -999999999999.99|**VST 9,5% DDV**|VAT Entry|VAT Amount|15, 313, 4313, 5313, 5140, 5040, 40, 140, 25, 11, 13, 111, 5011, 4011, 4013, 4111, 5111, 4040, 6013, 4613, 30|Type: Purchase
20|340|355|16|N|Flate-rate compensation 8%|right alignment, format -999999999999.99|**Pav nadomestilo**|VAT Entry|VAT Amount|29|Type: Purchase
21|357|516|160|AN|Notes - not mandatory|left alignment|**Opombe**|VAT Entry|Posting date||

----
----

**3. Output VAT Book Export - SI:**

Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name - IZPIS OBRAČUNANEGA DDV.TXT

Export VAT Entries where Amount or/and Base are not null. 

Export filters:
 - Posting Date - mandatory
 - Document No.

 No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV|VAT Identifier filter
--|--|--|--|------|-------|--------|----|-----|----|----|----------------------
1|1|4|4|N|VAT periodPosting Date in format <Month,2><Month,2>|**Odb**|VAT Entry|Posting Date
2|6|13|8|N|Posting date |format DDMMLLLL|**Dat knj**|VAT Entry|Posting Date
3|15|44|30|AN|Document No. |the first 30 characters, left alignment|**Številka listine**|VAT Entry|Document No.
4|46|53|8|N|Document date |format DDMMLLLL|**Dat lis**|VAT Entry|Document Date
5|55|104|50|AN|Customer name and address |the first 50 characters, left alignment|**Kupec**|Posted document /Vendor /Customer|Bill-to Name, Bill-to Address, Bill-to City, Bill-to Country/Region Code
6|106|125|20|AN|Customer VAT registration No. |the first 20 characters, left alignment|**IŠ za DDV**|VAT Entry|VAT Registration No.
7|127|142|16|N|The value of sales of goods and services excluding VAT |right alignment, format -999999999999.99|**Vred brez DDV**|VAT Entry|Base|9, 10, 12, 14, 16, 18, 112, 114, 116, 118|
8|144|159|16|N|The value of sales of goods and services in Slovenia from reverse charge VAT | right alignment, format -999999999999.99|**Vred za samoobd**|VAT Entry|Base|35, 36|
9|161|176|16|N|The value of exempt sales in EU without no right for deduction |right alignment, format -999999999999.99|**OD brez pravice**|VAT Entry|Base|8, 82|
10|178|193|16|N|The value of exempt sales in EU |right alignment, format -999999999999.99|**Op dob Skupnost**|VAT Entry|Base|37|
11|195|210|16|N|The value of exempt sales 3-Party EU |right alignment, format -999999999999.99|**Op tristr dob**|VAT Entry|Base|39|
12|212|227|16|N|The value of remote sales of goods |right alignment, format -999999999999.99|**Prod dalj**|VAT Entry|Base|38, 608|
13|229|244|16|N|The value of sales of goods with installation |right alignment, format -999999999999.99|**Prod mont**|VAT Entry|Base|708|
14|246|261|16|N|Calculated VAT 22% |right alignment, format -999999999999.99|**OBR 22% DDV**|VAT Entry|VAT Amount|14, 18, 114, 118, 27|
15|263|278|16|N|Calculated VAT 9,5% |right alignment, format -999999999999.99|**OBR 9,5% DDV**|VAT Entry|VAT Amount|12, 16, 112, 116|
16|280|295|16|N|Calculated VAT 22% for sales for goods in EU |right alignment, format -999999999999.99|**OBR 22% DDV BL S**|VAT Entry|VAT Amount|312, 314, 4312, 4314, 318, 5314|
17|297|312|16|N|Calculated VAT 22% for sales for services in EU |right alignment, format -999999999999.99|**OBR 22 % DDV ST S**|VAT Entry|VAT Amount|16, 110, 5016, 4016, 4110, 28|
18|314|329|16|N|Calculated VAT 9,5% for sales for goods in EU | right alignment, format -999999999999.99|**OBR 9,5% DDV BL S**|VAT Entry|VAT Amount VAT|311, 313, 4311, 4313, 317|
19|331|346|16|N|Calculated VAT 9,5% for sales for services in EU |right alignment, format -999999999999.99|**OBR 9,5% DDV ST S**|VAT Entry|VAT Amount VAT|15, 109|
20|348|363|16|N|Calculated VAT 22% for sales f goods and services in Slovenia from reverse charge VAT |right alignment, format -999999999999.99|**OBR 22% DDV samo**|VAT Entry|VAT Amount|5141, 5041, 26, 4026, 108, 41, 141, 5043, 43, 5143, 143, 4041, 4141, 4043, 4143, 44, 5044, 4108|
21|365|380|16|N|Calculated VAT 9,5% for sales f goods and services in Slovenia from reverse charge VAT |right alignment, format -999999999999.99|**OBR 9,5% DDV samo**|VAT Entry|VAT Amount|5140, 5040, 25, 40, 140, 107, 5042, 42, 5142, 142, 4040, 4140, 4042, 4142|
22|382|397|16|N|Calculated VAT for sales f goods and services from export |right alignment, format -999999999999.99|**OBR DDV uvoz**|VAT Entry|VAT Amount|6023, 6013, 4623, 4613, 6053, 6063|
23|399|414|16|N|The value of sales with right for deduction outside SI |right alignment, format -999999999999.99|**Vred obdavčljiv**|VAT Entry|Base|808|
24|416|575|160|AN|Notes - not mandatory |left alignment|**Opombe**|VAT Entry|Posting Date



-------------------------------------------------------------------------------------------------