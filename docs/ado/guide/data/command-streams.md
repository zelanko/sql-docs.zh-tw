---
title: 命令資料流 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9d1322d872d5e05de4c7f142804fe2f1390b9859
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700891"
---
# <a name="command-streams"></a>命令資料流
ADO 向來都支援指定的字串格式的命令輸入**CommandText**屬性。 或者，使用 ADO 2.7 或更新版本，您也可以使用資訊的資料流命令輸入藉由指定的資料流**CommandStream**屬性。 您可以指派 ADO **Stream**物件或任何支援 COM 的物件**IStream**介面。  
  
 命令資料流的內容只會從 ADO 到您的提供者，因此您的提供者必須支援這項功能運作的資料流所命令輸入。 例如，SQL Server 支援查詢的 XML 範本或 OpenXML TRANSACT-SQL 的延伸模組形式。  
  
 因為必須提供者所解譯的資料流的詳細資料，您必須設定來指定命令用語**方言**屬性。 值**方言**是包含 GUID，它由您的提供者所定義的字串。 如需有效值**方言**支援您的提供者，請參閱您的提供者文件。  
  
## <a name="xml-template-query-example"></a>XML 範本查詢範例  
 下列範例是以 VBScript 與 Northwind 資料庫。  
  
 首先，初始化並開啟**Stream**將用來包含查詢的資料流的物件：  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 查詢資料流的內容會是 XML 範本查詢。  
  
 範本查詢需要 sql 所識別的 XML 命名空間的參考： 前置詞\<sql:query > 標記。 SQL SELECT 陳述式是包含做為 XML 範本的內容，並指派給字串變數，如下所示：  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 接下來，將字串寫入資料流：  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 指派至 adoStreamQuery **CommandStream**屬性的 ADO**命令**物件：  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 指定命令語言**方言**，這表示 SQL Server OLE DB 提供者應如何解譯命令資料流。 提供者專屬 GUID 指定 dialect:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最後，執行查詢，並將結果傳回**資料錄集**物件：  
  
```  
Set objRS = adoCmd.Execute  
```
