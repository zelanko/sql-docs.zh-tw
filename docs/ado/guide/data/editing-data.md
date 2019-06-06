---
title: 編輯資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 998fd4ee425f1a4356bdc675b53b23247d89c3f8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700778"
---
# <a name="editing-data"></a>編輯資料
我們已說明如何使用 ADO 連接到資料來源執行命令，取得中的結果**Recordset**物件，並瀏覽**資料錄集**。 本節著重於下一個基本的 ADO 作業： 編輯資料。  
  
 本章節會繼續使用範例**資料錄集**中導入[檢查資料](../../../ado/guide/data/examining-data.md)，有一項重要變更。 下列程式碼用來開啟**資料錄集**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 程式碼的重要變更牽涉到設定**CursorLocation**屬性**連線**物件等於**adUseClient**在*GetNewConnection*函式 （在下一個範例中顯示），表示用戶端資料指標使用。 如需有關用戶端和伺服器端資料指標之間的差異的詳細資訊，請參閱[了解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。  
  
 **CursorLocation**屬性的**adUseClient**設定將資料指標的位置從資料來源 (SQL Server，在此情況下) 移至用戶端程式碼 （桌面工作站） 的位置。 此設定會強制在用戶端，來建立和管理資料指標上叫用戶端資料指標引擎，適用於 OLE DB 的 ADO。  
  
 您可能也注意**LockType**的參數**開放**方法變更為**Adlockpessimistic**。 這會在批次模式中開啟資料指標。 (提供者會快取多個變更，並將其寫入至基礎資料來源，只有當您呼叫時，才**UpdateBatch**方法。)對所做的變更**Recordset**將不會更新，直到資料庫中**UpdateBatch**呼叫方法。  
  
 最後，本節中的程式碼會使用 GetNewConnection 函式的修改的版本。 此版本的函式現在會傳回用戶端資料指標。 此函式看起來像這樣：  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 此章節包含下列主題。  
  
-   [編輯現有的記錄](../../../ado/guide/data/editing-existing-records.md)  
  
-   [新增記錄](../../../ado/guide/data/adding-records.md)  
  
-   [判斷支援的項目](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [使用 Delete 方法刪除記錄](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [替代方案：使用 SQL 陳述式](../../../ado/guide/data/alternatives-using-sql-statements.md)
