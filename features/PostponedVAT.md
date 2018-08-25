# Postponed VAT

For some countries (egg. Croatia) it is possible to correct sales VAT when approved Sales Credit Memo is received from customer and not when Credit Memo is posted. The Post and Correct Postponed VAT on Sales Credit Memos feature enables you to correct and postpone VAT on Sales Credit Memos to different GL account and with different setup in VAT entries, after you receive a receipt from the customer. Companies can reclaim VAT from the return of goods from a customer or from a discount granted after the invoice has been issued to a customer. To correct and postpone VAT on the Credit Memos on which the discount is granted after the invoice is issued, you must receive a written confirmation from the customer. For some countries (egg. Slovenia) only clause on the credit memo that VAT was subtracted is needed, so in that case functionality doesn't need to be turned on.

## Scope
User must be able to enter received date on Sales Credit Memo or directly in Journal Line. This action creates additional VAT Entry.

## Architectural Design

Sales Credit Memo is posted without VAT Date. When VAT date on credit memo is confirmed, realized VAT is posted on a new Posting Date. This will produce Journal Line and post automatically. After posting this value additional entry in VAT Entry is created. Feature can be used for all postings, not just Sales Credit Memos. Feature can eliminate the need for VAT Date field, if Reverse Charge posting can be solved without it.

For posting new entry logic must be placed in two codeunits: 
- Postponed VAT-Check
- Postponed VAT-Post

## Data Design

When posting VAT Entry in standard way (W1) it will produce one line from Document.

### Sales or Purchase Document

Posting Date|Document Type|Output Date|VAT Date|VAT %|VAT Amount
--|--|--|--|--|--
20.08.18|Sales Cr. Memo||01.09.18|20|-1.000,00

### VAT Entry - standard way

Posting Date|Amount|Base|Unrealized Amount|Unrealized Base|Remaining Amount|Remaining Base
-:|-:|-:|-:|-:|-:|-:
20.08.18|0,00|0,00|1.000,00|20.000,00|1.000,00|20.000,00

### VAT Entry - modified way

Posting Date|Amount|Base|Unrealized Amount|Unrealized Base|Remaining Amount|Remaining Base
-:|-:|-:|-:|-:|-:|-:
20.08.18|-1.000,00|-20.000,00|-1.000,00|-20.000,00|0,00|0,00
01.09.18|0,00|0,00|1.000,00	20.000,00|-1.000,00|-20.000,00

## Data Flow

Additional entry must be posted at the time of posting Gen. Journal Line. Investigate if event is appropriate to create additional VAT entry via TempGLEntryBuf:
``` PAS
"Gen. Jnl.-Post Line".OnBeforeInsertGLEntryBuffer(TempGLEntryBuf,GenJnlLine);
```

## User Interface

VAT Date should be editable on Posted Sales Cr. Memo as variable. After modifying VAT Date it should trigger posting via Journal. Journal already has VAT Date where user can address his posting.  