
=============================
**// Make centered Form //**
=============================

Sub Center_Button()

    ' Variabel untuk mengatur kolom pertama yang akan ditampilkan
    Dim firstCol As Integer
    Dim lastCol As Integer
    Dim colWidth As Integer
    Dim totalWidth As Integer
    Dim visibleCols As Integer
    Dim startCol As Integer

    ' Kolom pertama dan terakhir yang ingin DI tampilkan
    firstCol = Range("Q1").Column
    lastCol = Range("AA1").Column

    ' Hitung lebar total kolom Q hingga AA
    For i = firstCol To lastCol
        colWidth = Columns(i).ColumnWidth
        totalWidth = totalWidth + colWidth
    Next i

    ' Hitung jumlah kolom yang bisa terlihat di layar
    visibleCols = ActiveWindow.VisibleRange.Columns.Count

    ' Hitung kolom yang harus dimulai agar Q-AA berada di tengah
    startCol = firstCol - Int((visibleCols - (lastCol - firstCol + 1)) / 2)
    
    ' Pindahkan tampilan ke kolom yang dihitung
    ActiveWindow.ScrollColumn = startCol
    
    
    MsgBox "form centered !!", vbInformation


End Sub



=============================
**//Get Data From Sales Database and move it into main form for calculation//**
=============================

Sub Get_Data_Button()

    ' Define worksheets and ranges
    Dim wsMain As Worksheet
    Dim wsSheet1 As Worksheet
    Dim rngMain As Range
    Dim rngSheet1A As Range
    Dim cell As Range
    Dim matchCell As Range
    Dim total As Double
    Dim i As Long
    Dim totalRows As Long
    
    ' Set the worksheets
    Set wsMain = ThisWorkbook.Sheets("CG - MAIN")
    Set wsSheet1 = ThisWorkbook.Sheets("SALES")
    
    ' Define the ranges
    Set rngMain = wsMain.Range("R17:R300")
    Set rngSheet1A = wsSheet1.Range("A10:A300")
    
    ' Count the total number of rows to process
    totalRows = Application.WorksheetFunction.CountA(rngMain)
    
    ' Show the Progress Form and set initial progress
    ProgressForm.ProgressLabel.Width = 0
    ProgressForm.ProgressText.Caption = "Starting process..."
    ProgressForm.Show vbModeless
    
    ' Calculate maximum allowable width for the ProgressLabel within the ProgressForm
    Dim maxProgressWidth As Long
    maxProgressWidth = ProgressForm.Width - 30 ' Allowing for padding on the form
    
    ' Loop through the cells in CG - MAIN
    i = 1
    For Each cell In rngMain
        If cell.Value <> "" Then
            total = 0
            ' Loop through the range in Sheet1 to find matching values
            For Each matchCell In rngSheet1A
                If matchCell.Value = cell.Value Then
                    ' Add the corresponding value from column E in Sheet1
                    total = total + wsSheet1.Cells(matchCell.Row, "E").Value
                End If
            Next matchCell
            
            ' Place the total value in the corresponding cell in column Q
            wsMain.Cells(cell.Row, "Q").Value = total
        Else
            ' If the cell in column R is empty, make the corresponding cell in column Q empty
            wsMain.Cells(cell.Row, "Q").Value = ""
        End If
        
        ' Calculate progress percentage
        Dim progressPercent As Double
        progressPercent = i / totalRows
        
        ' Update progress label width and text
        ProgressForm.ProgressLabel.Width = progressPercent * maxProgressWidth
        ProgressForm.ProgressText.Caption = "Processing " & i & " of " & totalRows & " (" & Format(progressPercent * 100, "0") & "%)"
        
        ' Ensure ProgressLabel width does not exceed max width
        If ProgressForm.ProgressLabel.Width > maxProgressWidth Then
            ProgressForm.ProgressLabel.Width = maxProgressWidth
        End If
        
        ' Refresh display for smooth sync
        DoEvents

        i = i + 1
    Next cell
    
    ' Ensure final update to 100% when complete
    ProgressForm.ProgressLabel.Width = maxProgressWidth
    ProgressForm.ProgressText.Caption = "Processing complete! (100%)"

    ' Close the Progress Form
    Unload ProgressForm
    MsgBox "Data Moved to Main Form!", vbInformation




End Sub



=============================
**// Moving calculation data result from main form to order form //**
=============================


Sub Form_Order_Button()


    Dim wsMain As Worksheet
    Dim wsOrder As Worksheet
    Dim mainLastRow As Long
    Dim orderLastRow As Long
    Dim i As Long
    Dim j As Long

    ' Initialize worksheets
    Set wsMain = ThisWorkbook.Worksheets("CG - MAIN")
    Set wsOrder = ThisWorkbook.Worksheets("FORM ORDER")

    ' Find the last row in CG - MAIN and FORM ORDER
    mainLastRow = wsMain.Cells(wsMain.Rows.Count, 20).End(xlUp).Row ' Column T for 
    Ingredients_code
    orderLastRow = wsOrder.Cells(wsOrder.Rows.Count, 1).End(xlUp).Row ' Column A in FORM ORDER

    ' Show the Progress Form and set initial progress
    ProgressForm.ProgressLabel.Width = 0
    ProgressForm.ProgressText.Caption = "Starting process..."
    ProgressForm.Show vbModeless

    ' Loop through each Ingredients_code in CG - MAIN
    For i = 17 To mainLastRow
        Dim mainCode As String
        Dim estimationValue As Variant
        
        mainCode = wsMain.Cells(i, 20).Value ' Column T in CG - MAIN
        estimationValue = wsMain.Cells(i, 26).Value ' Column Z in CG - MAIN
        
        ' Match with each code in FORM ORDER
        For j = 4 To orderLastRow
            If wsOrder.Cells(j, 1).Value = mainCode Then ' Column A in FORM ORDER
                ' Place Estimation in Column G and H in FORM ORDER
                wsOrder.Cells(j, 7).Value = estimationValue ' Column G
                wsOrder.Cells(j, 8).Value = estimationValue / 4 ' Column H
                Exit For ' Exit loop once a match is found
            End If
        Next j
        
        ' Update progress
        Dim progressPercent As Double
        progressPercent = (i - 17 + 1) / (mainLastRow - 16) ' Calculate progress percentage
        ProgressForm.ProgressLabel.Width = progressPercent * (ProgressForm.Width - 30) ' Update label width
        ProgressForm.ProgressText.Caption = "Processing " & (i - 16) & " of " & (mainLastRow - 16) & " (" & Format(progressPercent * 100, "0") & "%)"
        
        ' Refresh display for smooth sync
        DoEvents
    Next i

    ' Final update for completion
    ProgressForm.ProgressLabel.Width = ProgressForm.Width - 30
    ProgressForm.ProgressText.Caption = "Processing complete! (100%)"

    ' Close the Progress Form
    Unload ProgressForm
    MsgBox "Data Moved to Form Order !!", vbInformation



End Sub




=============================
**//Print Out the Order form into pdf format//**
=============================


Sub Print_Out_Button()


    Dim ws As Worksheet
    Dim lastRow As Long
    Dim pdfPath As String
    Dim pdfFileName As String

    ' Tentukan worksheet
    Set ws = ThisWorkbook.Sheets("FORM ORDER")
    
    ' Cari baris terakhir pada kolom A
    lastRow = ws.Cells(ws.Rows.Count, "A").End(xlUp).Row
    
    ' Tentukan path untuk menyimpan PDF di desktop
    pdfPath = Environ("USERPROFILE") & "\Desktop\"
    pdfFileName = "form order.pdf"
    
    ' Hapus file jika sudah ada
    On Error Resume Next
    Kill pdfPath & pdfFileName
    On Error GoTo 0

    ' Tentukan rentang yang akan dicetak
    Dim rng As Range
    Set rng = ws.Range("A2:H" & lastRow)

    ' Ekspor rentang ke PDF
    rng.ExportAsFixedFormat Type:=xlTypePDF, Filename:=pdfPath & pdfFileName, Quality:=xlQualityStandard, _
                            IncludeDocProperties:=True, IgnorePrintAreas:=False, _
                            OpenAfterPublish:=False

    ' Pemberitahuan selesai
    MsgBox "PDF berhasil disimpan di " & pdfPath & pdfFileName



End Sub

