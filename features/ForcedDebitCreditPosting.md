# Forced Debit / Credit Posting

Forced Debit/Credit posting functionality enables checking the side of posting and force posting to the side, set on the account when Debit or Credit posting is set on General ledger account. (Debit/Credit Inventory, report 1001, report item card)

> Range: 13.062.571..13.062.580

## Scope

Posting to GL must be forced in some cases to poste on correct side: debit or credit. 

## Architectural Design 

In base code every financial transaction ends in General Journal Line. And from there into G/L Entry. Credit or Debit side are chosen in combination from Setup and Code.

## Data Flow

When inserting to G/L Entry there is event which can be used for changing entry:

``` PAS
LOCAL [IntegrationEvent] OnBeforeInsertGLEntryBuffer(VAR TempGLEntryBuf : TEMPORARY Record "G/L Entry";VAR GenJournalLine : Record "Gen. Journal Line")
```

Following lines can describe the way for updating correct side: 

``` PAS
[EventSubscriber] CheckDebitCredit(VAR TempGLEntryBuf : TEMPORARY Record "G/L Entry";VAR GenJournalLine : Record "Gen. Journal Line");
//DCA
WITH GLAccount DO BEGIN
  GET(TempGLEntryBuf."G/L Account No.");
  IF "Debit/Credit" = "Debit/Credit"::Both THEN
    EXIT;

  IF CLOSINGDATE(TempGLEntryBuf."Posting Date") = TempGLEntryBuf."Posting Date" THEN
    CASE "Debit/Credit" OF
      "Debit/Credit"::Debit : "Debit/Credit" := "Debit/Credit"::Credit;
      "Debit/Credit"::Credit : "Debit/Credit" := "Debit/Credit"::Debit;
    END;

  CASE "Debit/Credit" OF
    "Debit/Credit"::Debit:
       BEGIN
          TempGLEntryBuf."Debit Amount" := TempGLEntryBuf.Amount;
          TempGLEntryBuf."Credit Amount" := 0;
          TempGLEntryBuf."Add.-Currency Debit Amount" := TempGLEntryBuf."Additional-Currency Amount";
          TempGLEntryBuf."Add.-Currency Credit Amount" := 0;
       END;
    "Debit/Credit"::Credit:
       BEGIN
          TempGLEntryBuf."Debit Amount" := 0;
          TempGLEntryBuf."Credit Amount" := -TempGLEntryBuf.Amount;
          TempGLEntryBuf."Add.-Currency Debit Amount" := 0;
          TempGLEntryBuf."Add.-Currency Credit Amount" := -TempGLEntryBuf."Additional-Currency Amount";
       END;
  END;
END;
```

## User Interface

There is no additional user interface.