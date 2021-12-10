---
title: Generate Progress Bar for PPT
author: xueyong
date: 2021-11-13 11:33:00 +0800
categories: [Tools, PPT]
tags: [office, PPT, slides, progress bar]
math: true
mermaid: true

---

This post is to show how to generate pogress bar for PPT using Visual Basic macro.

## Create VBA (Visual Basic Application)
### 1. Open the PowerPoint presentation that you would like to create a progress bar for. 
### 2. Once it’s open, click the “View” tab, then select “Macros.” OR use shortcuts `Alt` + `F11` to open the “Microsoft Visual Basic for Applications (VBA)” window.
### 3. Copy the VB code and run.
The function of `ProgressBar` is as follows.

```vb
Sub ProgressBar()

    Dim mySlides As Slides
    Dim pageBar As ShapeRange
    Dim pageSHower As Shape
    Dim pageWidth, pageHeight, pageStep
    Dim MyArray() As Variant  '增加一个数组以便统计隐藏的幻灯片
    Dim i, j, k
    j = 0
    k = 0

    Set mySlides = Application.ActivePresentation.Slides

    pageWidth = Application.ActivePresentation.SlideMaster.Width
    pageHeight = Application.ActivePresentation.SlideMaster.Height
    ' pageStep = pageWidth / mySlides.Count

    ReDim MyArray(mySlides.Count, 0)
    
    For i = 1 To mySlides.Count '统计隐藏的幻灯片数
        If mySlides.Item(i).SlideShowTransition.Hidden = True Then
            j = j + 1
            MyArray(i, 0) = 1
        Else
            MyArray(i, 0) = 0
        End If
    Next

    '除去首页和隐藏的幻灯片后计算进度条长度增量
    If mySlides.Count - 1 - j > 0 Then
        pageStep = pageWidth / (mySlides.Count - 1 - j)
    Else
        pageStep = 0
    End If

    On Error Resume Next

    For i = 1 To mySlides.Count    ' 改为从1开始
        k = k + MyArray(i, 0)      ' 计算当前隐藏的幻灯片数
        Set pageBar = mySlides.Item(i).Shapes.Range(Array())
        Set pageBar = _
           mySlides.Item(i).Shapes.Range(Array("RectanglePageNum"))

        If IsNull(pageBar) Or pageBar.Count = 0 Then GoTo newBar
        Set pageSHower = pageBar.Item(1)
        GoTo nextPage

newBar:
        Set pageSHower = mySlides.Item(i).Shapes.AddShape( _
                           msoShapeRectangle, 0, _
                           pageHeight - 4, i * pageStep, 4)
        pageSHower.Name = "RectanglePageNum"

nextPage:
        'pageSHower.Fill.ForeColor.RGB = RGB(246, 202, 5)
        pageSHower.Fill.ForeColor.RGB = RGB(56, 93, 138) '设置颜色color of progress bar. This color is NTU blue.
        pageSHower.Line.Visible = msoFalse
        ' pageSHower.Width = i * pageStep
        ' 计算进度条长度时除去首页和隐藏的幻灯片
        pageSHower.Width = (i - 1 - k) * pageStep
        pageSHower.Top = pageHeight - 3 '位置location of progress bar
        pageSHower.Left = 0
        pageSHower.Height = 3 '高度height of progress bar
        ' 删除首页和隐藏的幻灯片的进度条
        If i = 1 Or MyArray(i, 0) = 1 Then pageSHower.Delete
    Next
End Sub
```

### 4. Save as .pptm
To save a presentation that contains VBA macros, You have to use the file as .pptm format.
