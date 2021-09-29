# Next Search Catalog notices and slips backup

## Instructions:

Create a folder on your c:\ drive called "git"

Add 1 folder to c:\git for each of your libraries where the folder names are the same as your branchcodes

Add 1 folder to c:\git called "AAAAA"

Run this SQL (Next Search Catalog report 2960), save it as a csv spreadsheet, open the file in Excel

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

Check to make sure C:\git\ has one folder for each branch already created and one folder called "AAAAA"

With the csv file open in Excel, run this VBA macro:

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

This macro should save the contents of coulmn B in a text file in c:\git.  The title of each file should be based on column A.  Each text file should be saved in the folder for the branchcode that the notice or slip is for.  If the slip is not assigned to a specific branchcode, then it will be saved in c:\git\AAAAA

Move the contents of c:\git to the local folder for your repository and then use git to sync the updated information with your repository.

-----

Use the duplicate receipts and notices report to identify duplicate notices and receipts as needed.
