---
description: 編輯資料
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 01f5f2010491e394addd37511ead8b7ea20136c1
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806878"
---
# <a name="editing-data"></a>編輯資料
我們已說明如何使用 ADO 連接到資料來源、執行命令、取得 **記錄集** 物件中的結果，以及在 **記錄集**內導覽。 本節著重于下一個基本 ADO 作業：編輯資料。  
  
 本節將繼續使用在[檢查資料](./examining-data.md)時所引進的範例**記錄集**，但有一項重要變更。 下列程式碼用來開啟 **記錄集**：  
  
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
  
 程式碼的重要變更包括將**連接**物件的**CursorLocation**屬性設定為*GetNewConnection*函式中的**adUseClient** ， (下一個範例) 中所示，這表示使用用戶端資料指標。 如需用戶端和伺服器端資料指標之間差異的詳細資訊，請參閱 [瞭解資料指標和鎖定](./understanding-cursors-and-locks.md)。  
  
 **CursorLocation**屬性的**adUseClient**設定會將資料指標的位置從資料來源移 (SQL Server，在此案例中) 至桌面工作站)  (的用戶端程式代碼位置。 這項設定會強制 ADO 針對用戶端上的 OLE DB 叫用用戶端資料指標引擎，以便建立和管理資料指標。  
  
 您也可能已經注意到， **Open**方法的**LockType**參數已變更為**adLockBatchOptimistic**。 這會以批次模式開啟資料指標。  (提供者會快取多項變更，而且只有在您呼叫**updatebatch**方法時，才會將這些變更寫入基礎資料來源。在呼叫**updatebatch**方法之前，將不會在資料庫中更新對**記錄集**所做的變更 ) 。  
  
 最後，本節中的程式碼會使用修改過的 GetNewConnection 函式版本。 此版本的函式現在會傳回用戶端資料指標。 函數看起來像這樣：  
  
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
  
-   [編輯現有的記錄](./editing-existing-records.md)  
  
-   [新增記錄](./adding-records.md)  
  
-   [判斷支援的項目](./determining-what-is-supported.md)  
  
-   [使用 Delete 方法刪除記錄](./deleting-records-using-the-delete-method.md)  
  
-   [替代方案：使用 SQL 陳述式](./alternatives-using-sql-statements.md)