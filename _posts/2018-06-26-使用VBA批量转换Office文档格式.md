---
layout: post
title: "使用VBA批量转换Office文档格式"
date: 2018-06-26 19:15:10
categories: Code
tags: VBA Office Batch Convert
excerpt: 例如，转换doc到docx
---

* content
{:toc}

### 代码

```visualbasic
Sub FileConverter()
'==============================
sourceType = "doc"
targetType = "docx"
oldToNew = True
delSourceFile = True
'==============================
If oldToNew = True Then
targetFormat = 12
Else
targetFormat = 0
End If
Dim myDialog As FileDialog
Dim oFile As Variant
Set myDialog = Application.FileDialog(msoFileDialogFilePicker)
Set myFileSystem = CreateObject("scripting.filesystemobject")
With myDialog
.Filters.Clear
.Filters.Add sourceType + " 文件", "*." + sourceType, 1
.AllowMultiSelect = True
If .Show = -1 Then
For Each oFile In .SelectedItems
With Documents.Open(oFile)
.SaveAs FileName:=Replace(oFile, sourceType, targetType), FileFormat:=targetFormat
.Close
End With
If delSourceFile = True Then
myFileSystem.deletefile (oFile)
End If
Next
End If
End With
End Sub
```