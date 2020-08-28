---
description: 命令資料流
title: 命令資料流程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: rothja
ms.author: jroth
ms.openlocfilehash: 2ae54835836fecdfbf3b026fe9e6a701a5602d3d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991539"
---
# <a name="command-streams"></a>命令資料流
ADO 一律支援 **CommandText** 屬性所指定之字串格式的命令輸入。 另一種方法是使用 ADO 2.7 或更新版本，您也可以藉由將資料流程指派給 **CommandStream** 屬性，來使用命令輸入的資訊串流。 您可以指派 ADO **資料流程** 物件或任何支援 COM **IStream** 介面的物件。  
  
 命令資料流程的內容只會從 ADO 傳遞給您的提供者，因此您的提供者必須支援串流的命令輸入，這項功能才能運作。 例如，SQL Server 支援 XML 範本形式的查詢或 Transact-sql 的 OpenXML 延伸。  
  
 因為資料流程的詳細資料必須由提供者來解讀，所以您必須藉由設定 **方言** 屬性來指定命令方言。 **方言**的值是包含 GUID 的字串，由您的提供者定義。 如需提供者所支援的正確 **方言** 值的詳細資訊，請參閱您的提供者檔。  
  
## <a name="xml-template-query-example"></a>XML 範本查詢範例  
 下列範例是以 VBScript 撰寫給 Northwind 資料庫。  
  
 首先，初始化並開啟將用來包含查詢資料流程的 **資料流程** 物件：  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 查詢資料流程的內容將會是 XML 範本查詢。  
  
 範本查詢需要由標記的 sql：前置詞所識別之 XML 命名空間的參考 \<sql:query> 。 SQL SELECT 語句會包含為 XML 範本的內容，並指派給字串變數，如下所示：  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 接下來，將字串寫入資料流程：  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 將 adoStreamQuery 指派給 ADO**命令**物件的**CommandStream**屬性：  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 指定命令語言 **方言**，指出 SQL Server OLE DB 提供者應該如何解讀命令資料流程。 提供者特定 GUID 所指定的方言：  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最後，執行查詢，並將結果傳回到 **記錄集** 物件：  
  
```  
Set objRS = adoCmd.Execute  
```
