---
layout: post
title: Iron Python and Excel
---

So how do we interact with Excel in Grasshopper, and more particularly, to call a macro that's stored inside the xlsm file?

First, we can use bumblebee, a grasshopper plugin suite that interfaces with Excel.
![My helpful screenshot]({{ site.url }}/images/ladybug_grasshopper_butterfly_honeybee.png)

Just look at all these cute grasshopper plugins!

The way to do it with Python outside Grasshoper is using win32com.client
    import os
    import win32com.client

    if os.path.exists("excelsheet.xlsm"):
        xl=win32com.client.Dispatch("Excel.Application")
        xl.Workbooks.Open(Filename="C:\Full Location\To\excelsheet.xlsm", ReadOnly=1)
        xl.Application.Run("excelsheet.xlsm!modulename.macroname")
    ##    xl.Application.Save() # if you want to save then uncomment this line and change delete the ", ReadOnly=1" part from the open function.
        xl.Application.Quit() # Comment this out if your excel script closes
        del xl
        
In Grasshopper's IronPython, we can use clr to reference the Excel COM object
    import os
    import clr

    clr.AddReferenceByName('Microsoft.Office.Interop.Excel, Version=11.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c')
    from Microsoft.Office.Interop import Excel

    ex = Excel.ApplicationClass()   
    ex.Visible = True
    ex.DisplayAlerts = False   

    workbook = ex.Workbooks.Open('D:/Eric/Projects/Earthworm/Piglet Files/test.xlsm')
    ex.Application.Run("test.xlsm!Module1.Run")
   
Very useful information here:
    http://www.ironpython.info/index.php?title=Interacting_with_Excel
    
Or else, we can use python library xlrd, xlwt and xlutils.
