# nexpress-notices-and-slips

## Instructions:

Run this SQL (Next Search Catalog report 2960) and save as a spreadsheet.

```sql

SELECT
  Concat(
    If(letter.branchcode = " ", "AAAAA", letter.branchcode),
    "\\",
    letter.code,
    ".",
    letter.lang,
    ".",
    letter.message_transport_type
  ) AS FILE,
  Concat(
    Concat(
      If(letter.branchcode = " ", "AAAAA", letter.branchcode),
      ".",
      letter.code,
      ".",
      letter.lang,
      ".",
      letter.message_transport_type,
      ".txt"
    ),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    Concat("Name: ", letter.name),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    Concat("-----"),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    letter.title,
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    Concat("-----"),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    Concat("Message content:"),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    Concat("----------"),
    CHAR(13), CHAR(10), CHAR(13), CHAR(10),
    letter.content
  ) AS CONTENTS
FROM
  letter
GROUP BY
  FILE
ORDER BY
FILE

```


Make sure C:\git\ has one folder for each branch already created and one folder called "AAAAA" for any notices that are not assigned to a specific branch.

Open the csv file in Excel and run this VBA macro:

```vba

Sub WriteTotxtNotices()

Const forReading = 1, forAppending = 3, fsoForWriting = 2
Dim fs, objTextStream, sText As String
Dim lLastRow As Long, lRowLoop As Long, lLastCol As Long, lColLoop As Long

lLastRow = Cells(Rows.Count, 1).End(xlUp).Row

For lRowLoop = 1 To lLastRow

    Set fs = CreateObject("Scripting.FileSystemObject")
    Set objTextStream = fs.opentextfile("c:\git\" & Cells(lRowLoop, 1) & ".txt", fsoForWriting, True)

    sText = ""

    For lColLoop = 2 To 2
        sText = sText & Cells(lRowLoop, lColLoop) & Chr(10) & Chr(10)
    Next lColLoop

    objTextStream.writeline (Left(sText, Len(sText) - 1))


    objTextStream.Close
    Set objTextStream = Nothing
    Set fs = Nothing

Next lRowLoop

End Sub

```

This should give you 1 text file for each row in the report saved in C:\git\.  Each text file represents 1 notice/slip from Koha.

Save these in the github folder and run git to sync with the online repository.
