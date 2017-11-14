---
title: "使用連接物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da71dc67a1fd6a17f75c5aceaf7a88dce7d328ab
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-connection-object"></a>使用連接物件
才能開啟**連接**物件，您必須定義特定資料來源和連接類型的相關資訊。 大部分的這項資訊由*ConnectionString*參數[Open 方法](../../../ado/reference/ado-api/open-method-ado-connection.md)上**連接**物件，或由[ConnectionString屬性](../../../ado/reference/ado-api/connectionstring-property-ado.md)上**連接**物件。 連接字串包含分號，以單引號括住值的引數/值組的清單。 例如：  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  您也可以指定 ODBC 資料來源名稱 (DSN) 或資料連結 (UDL) 檔案中的連接字串。 如需名稱 （dsn） 的詳細資訊，請參閱[管理資料來源](../../../odbc/admin/managing-data-sources.md)ODBC 程式設計人員參考中。 如需 Udl 的詳細資訊，請參閱[資料連結 API 概觀](http://msdn.microsoft.com/en-us/95c180ea-bd4f-4dca-b95a-576afd135bbc)OLE DB 程式設計人員參考中。  
  
 一般而言，您藉由呼叫，會在建立連接時**c**以適當的方法*連接字串*做為其參數。 範例是以下列 Visual Basic 程式碼片段所示：  
  
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
  
 這裡**oRs.Open**採用**連接**物件 (*oConn*) 變數的值作為其*ActiveConnection*參數。 此外， **Connection.CursorLocation**屬性採用的預設值**adUseServer**。 若要將此相比[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)如上一節的範例。 下列指示會導致執行階段錯誤。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```

