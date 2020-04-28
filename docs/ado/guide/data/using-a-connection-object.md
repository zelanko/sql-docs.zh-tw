---
title: 使用 Connection 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f1b867e1870b81641c7cea09d9a8fb3accfcc01
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923640"
---
# <a name="using-a-connection-object"></a>使用 Connection 物件
開啟**連接**物件之前，您必須定義有關資料來源和連線類型的特定資訊。 這大部分的資訊都是由**connection**物件上[Open 方法](../../../ado/reference/ado-api/open-method-ado-connection.md)的*ConnectionString*參數所持有，或是由**connection**物件上的[connectionstring 屬性](../../../ado/reference/ado-api/connectionstring-property-ado.md)所保留。 連接字串是由以分號分隔的引數/值組清單所組成，其中的值以單引號括住。 例如：  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  您也可以在連接字串中指定 ODBC 資料來源名稱（DSN）或資料連結（UDL）檔案。 如需有關 Dsn 的詳細資訊，請參閱管理 ODBC 程式設計人員參考中的[資料來源](../../../odbc/admin/managing-data-sources.md)。 如需 Udl 的詳細資訊，請參閱 OLE DB 程式設計人員參考中的[資料連結 API 總覽](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc)。  
  
 一般來說，您可以呼叫**connection. Open**方法來建立連接，並以適當的*連接字串*做為其參數。 範例如下列 Visual Basic 程式碼片段所示：  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 在此**or 中**，會使用**Connection**物件（*OConn*）變數作為其*ActiveConnection*參數的值。 此外， **CursorLocation**屬性會假設預設值是**adUseServer**。 與上一節中的[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)範例相反。 下列指令會導致執行階段錯誤。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
