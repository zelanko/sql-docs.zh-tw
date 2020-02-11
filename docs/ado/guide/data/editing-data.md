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
ms.openlocfilehash: 8e8fd90849b8e046a7f4fe5d158d4594e612c91f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925496"
---
# <a name="editing-data"></a>編輯資料
我們已說明如何使用 ADO 連接到資料來源、執行命令、取得**記錄集**物件中的結果，以及在**記錄集中**流覽。 本節著重于下一個基本 ADO 作業：編輯資料。  
  
 這一節會繼續使用在[檢查資料](../../../ado/guide/data/examining-data.md)時所引進的範例**記錄集**，但有一項重要的變更。 下列程式碼是用來開啟**記錄集**：  
  
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
  
 對程式碼的重要變更牽涉到在*GetNewConnection*函式中，將**連接**物件的**CursorLocation**屬性設定為等於**adUseClient** （在下一個範例中顯示），這表示使用的是用戶端資料指標。 如需有關用戶端和伺服器端資料指標之間差異的詳細資訊，請參閱[瞭解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。  
  
 **CursorLocation**屬性的**adUseClient**設定會將游標的位置從資料來源（在此案例中為 SQL Server）移至用戶端程式代碼的位置（桌面工作站）。 這項設定會強制 ADO 針對用戶端上的 OLE DB 叫用用戶端資料指標引擎，以便建立和管理資料指標。  
  
 您可能也注意到**Open**方法的**LockType**參數已變更為**adLockBatchOptimistic**。 這會以批次模式開啟資料指標。 （提供者會快取多個變更，並只有在您呼叫**UpdateBatch**方法時，才會將它們寫入基礎資料來源）。等到呼叫**UpdateBatch**方法之後，才會在資料庫中更新對**記錄集**所做的變更。  
  
 最後，本節中的程式碼會使用 GetNewConnection 函數的修改版本。 這個版本的函式現在會傳回用戶端資料指標。 函式看起來像這樣：  
  
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
