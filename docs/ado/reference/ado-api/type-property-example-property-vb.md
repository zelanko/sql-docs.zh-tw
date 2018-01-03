---
title: "輸入屬性的範例 （屬性） (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords: Type property [property] [ADO], Visual Basic example
ms.assetid: 2ee8e4c5-1d66-4a77-8892-6dad7e07e611
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca949b82660a87d3688bfc18e54fcb61a78b2b14
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="type-property-example-property-vb"></a>型別屬性範例 （屬性） (VB)
這個範例會示範[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性。 它是一種模型的公用程式清單的名稱和類型的集合，例如[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)，[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)等等。  
  
 我們不需要開啟[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)存取其**屬性**集合; 它們消失時**資料錄集**物件具現化。 不過，設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**新增數個動態屬性，**資料錄集**物件的**屬性**集合，讓範例更有趣。 基於說明目的，我們明確使用[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性來存取每個[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。  
  
```  
'BeginTypePropertyVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' recordset variables  
    Dim rst As ADODB.Recordset  
    Dim prop As ADODB.Property  
     ' property variables  
    Dim ix As Integer  
    Dim strMsg As String  
  
     ' create client-side recordset  
    Set rst = New ADODB.Recordset  
    rst.CursorLocation = adUseClient  
     ' enumerate property types  
    For ix = 0 To rst.Properties.Count - 1  
        Set prop = rst.Properties.Item(ix)  
        Select Case prop.Type  
           Case adBigInt  
              strMsg = "adBigInt"  
           Case adBinary  
              strMsg = "adBinary"  
           Case adBoolean  
              strMsg = "adBoolean"  
           Case adBSTR  
              strMsg = "adBSTR"  
           Case adChapter  
              strMsg = "adChapter"  
           Case adChar  
              strMsg = "adChar"  
           Case adCurrency  
              strMsg = "adCurrency"  
           Case adDate  
              strMsg = "adDate"  
           Case adDBDate  
              strMsg = "adDBDate"  
           Case adDBTime  
              strMsg = "adDBTime"  
           Case adDBTimeStamp  
              strMsg = "adDBTimeStamp"  
           Case adDecimal  
              strMsg = "adDecimal"  
           Case adDouble  
              strMsg = "adDouble"  
           Case adEmpty  
              strMsg = "adEmpty"  
           Case adError  
              strMsg = "adError"  
           Case adFileTime  
              strMsg = "adFileTime"  
           Case adGUID  
              strMsg = "adGUID"  
           Case adIDispatch  
              strMsg = "adIDispatch"  
           Case adInteger  
              strMsg = "adInteger"  
           Case adIUnknown  
              strMsg = "adIUnknown"  
           Case adLongVarBinary  
              strMsg = "adLongVarBinary"  
           Case adLongVarChar  
              strMsg = "adLongVarChar"  
           Case adLongVarWChar  
              strMsg = "adLongVarWChar"  
           Case adNumeric  
              strMsg = "adNumeric"  
           Case adPropVariant  
              strMsg = "adPropVariant"  
           Case adSingle  
              strMsg = "adSingle"  
           Case adSmallInt  
              strMsg = "adSmallInt"  
           Case adTinyInt  
              strMsg = "adTinyInt"  
           Case adUnsignedBigInt  
              strMsg = "adUnsignedBigInt"  
           Case adUnsignedInt  
              strMsg = "adUnsignedInt"  
           Case adUnsignedSmallInt  
              strMsg = "adUnsignedSmallInt"  
           Case adUnsignedTinyInt  
              strMsg = "adUnsignedTinyInt"  
           Case adUserDefined  
              strMsg = "adUserDefined"  
           Case adVarBinary  
              strMsg = "adVarBinary"  
           Case adVarChar  
              strMsg = "adVarChar"  
           Case adVariant  
              strMsg = "adVariant"  
           Case adVarNumeric  
              strMsg = "adVarNumeric"  
           Case adVarWChar  
              strMsg = "adVarWChar"  
           Case adWChar  
              strMsg = "adWChar"  
           Case Else  
              strMsg = "*UNKNOWN*"  
        End Select  
            'show results  
        Debug.Print "Property " & ix & ": " & prop.Name & _  
                    ", Type = " & strMsg  
    Next ix  
  
    ' clean up  
    Set rst = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    Set rst = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndTypePropertyVB  
```  
  
## <a name="see-also"></a>請參閱  
 [屬性物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
