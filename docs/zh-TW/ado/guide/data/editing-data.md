---
title: 編輯資料 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e669880691cd61db355bdceb9323f51ebef1a6f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="editing-data"></a>編輯資料
我們解釋如何使用 ADO 連接到資料來源、 執行命令，取得結果**資料錄集**物件，並在瀏覽**資料錄集**。 本節著重於下一個基本的 ADO 作業： 編輯資料。  
  
 本節會繼續使用範例**資料錄集**中導入[檢查資料](../../../ado/guide/data/examining-data.md)，有一項重要變更。 下列程式碼用來開啟**資料錄集**:  
  
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
  
 程式碼的重要變更包括設定**CursorLocation**屬性**連接**物件等於**adUseClient**中*GetNewConnection*函式 （在下一個範例中顯示），表示用戶端資料指標使用。 如需用戶端和伺服器端資料指標之間的差異的詳細資訊，請參閱[了解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。  
  
 **CursorLocation**屬性的**adUseClient**設定資料來源 (SQL Server，在此情況下) 的游標位置移至用戶端程式碼 （桌面工作站） 的位置。 這項設定會強制在用戶端，才能建立與管理資料指標上叫用戶端資料指標引擎的 OLE DB ADO。  
  
 您可能也注意**LockType**參數**開啟**方法變更為**Adlockpessimistic**。 這會在批次模式中開啟資料指標。 (提供者會快取多個變更，並將它們寫入基礎資料來源，只有當您呼叫**UpdateBatch**方法。)對所做的變更**資料錄集**將不會更新，直到資料庫在**UpdateBatch**方法呼叫。  
  
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
