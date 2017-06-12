
---
layout: post
title: Pandas vs Excel VBA
---

Today I had to write an ad hoc script with VBA. Only now do I realize how rudimental the functions in VBA are when compared to python! I wrote the script in Excel with around 120 lines, and only 19 lines with python! There's no easy way to check if an element is in an array in vba, nor forward fill, nor split by id, but all these are found in python. 

Some comparisons:

1. Is an element in an array
VBA:
    Private Function isSoilOK(Soil As String)
        Dim SoilOK(6) As String
        SoilOK(0) = "I(B)"
        SoilOK(1) = "I/II(B)"
        SoilOK(2) = "II(B)"
        SoilOK(3) = "II/III(B)"
        SoilOK(4) = "III(B)"
        SoilOK(5) = "III/II(B)"
        SoilOK(6) = "III/II/I(B)"
        If IsInArray(Soil, SoilOK) Then
            isSoilOK = True
        Else
            isSoilOK = False
        End If
    End Function
    Private Function IsInArray(stringToBeFound As String, arr As Variant) As Boolean
      IsInArray = (UBound(Filter(arr, stringToBeFound)) > -1)
    End Function
    

Python:

    soil = pd.Series(['I(B)','II(B)','III(B)','II/I(B)','I/II(B)','III/II(B)','II/III(B)','III/II/I(B)']
    group[group.GEOL.isin(soil.values)]
    
2. Forward Fill
VBA:
    Dim LastUCS As Double
    Dim LastRQD As Double
    LastUCS = 0
    LastRQD = 0
    Dim BH_ID As String
    BH_ID = Cells(StartRow, "B").Value
    For i = StartRow To EndRow
        Dim UCS As Double
        Dim RQD As Double
        Dim GEOL As String
        UCS_temp = Cells(i, "V").Value
        RQD_temp = Cells(i, "P").Value
        GEOL = CStr(Cells(i, "AH").Value)
        If Not IsNumeric(UCS_temp) Then
            UCS = LastUCS
        Else
            UCS = CDbl(UCS_temp)
            LastUCS = UCS ''Update LastUCS
        End If
        If Not IsNumeric(RQD_temp) Then
            RQD = LastRQD
        Else
            RQD = CDbl(RQD_temp)
            LastRQD = RQD ''Update LastRQD
        End If
    Next
    

Python:

    group.UCS = group.UCS.fillna(method='ffill')
    group.RQD = group.RQD.fillna(method='ffill')
    
    
3. Split-Apply-Combine
VBA:
    
    Dim BH_Start As Long
    BH_Start = 4
    Dim CurrentBH_ID As String
    CurrentBH_ID = DataWS.Cells(BH_Start, "B").Value
    For i = BH_Start To DataWS.Cells(Rows.Count, 1).End(xlUp).Row + 1
        Dim BH_ID As String
        BH_ID = DataWS.Cells(i, "B").Value
        If Not BH_ID = Current_BHID Then
            Dim StartRow As Long
            Dim EndRow As Long
            StartRow = BH_Start
            EndRow = i - 1
            Dim RQD As Double, UCS As Double
            Dim RockheadRow As Long
            RockheadRow = Rockhead(StartRow, EndRow, RQDLimit, UCSLimit, RQD, UCS)
            Dim ResultsRow As Long
            ResultsRow = ResultWS.Cells(Rows.Count, 1).End(xlUp).Row + 1
            ResultWS.Cells(ResultsRow, 1).Value = Current_BHID
            BH_Start = i
            Current_BHID = BH_ID
        End If
    Next
    
Python

    gb = df.groupby(['id'], as_index=False)
    
    
Well.. Python is the clear winner here. The only thing is, probably because I'm not used to using Python, I often have to go back to Excel to look at the values to check whether my python code is giving me the correct results, and I found a few mistakes that I might not have found using Excel. Excel's GUI is still very user-friendly to visualize data.


Full code here:
https://github.com/bongster21/rockhead
    
  
