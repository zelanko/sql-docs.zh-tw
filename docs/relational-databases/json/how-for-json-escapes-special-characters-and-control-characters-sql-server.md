---
title: "FOR JSON 如何逸出特殊字元和控制字元 (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, 特殊字元"
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# FOR JSON 如何逸出特殊字元和控制字元 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主題說明 **FOR JSON** 子句如何逸出特殊字元，並在 JSON 輸出中代表控制字元。  
  
## 逸出特殊字元  
 **FOR JSON** 子句會以 `\` 逸出 JSON 輸出中的特殊字元，如下表所示。 在屬性名稱和它們的值中都會發生這項逸出。  
  
|**特殊字元**|**編碼的序列**|  
|---------------------------|--------------------------|  
|引號 (")|\\"|  
|反斜線 (\\)|\\\|  
|斜線 (/)|\\/|  
|退格鍵|\b|  
|換頁字元|\f|  
|新行|\n|  
|歸位字元|\r|  
|水平 Tab 鍵|\t|  
  
## 控制字元  
 **FOR JSON** 子句會以 `\u<code>` 格式代表 JSON 輸出中的特殊字元，如下表所示。  
  
|**控制字元**|**編碼的序列**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## 範例  
 以下是 **FOR JSON** 子句的範例，其中包含逸出和控制字元。  
  
 查詢：  
  
```tsql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 結果：  
  
```json  
{  
   "KEY\\\t\/\"":"VALUE\\\t\/\r\n\"",  
   "0":"\u0000",  
   "1":"\u0001",  
  "31":"\u001f“  
}  
```  
  
## 另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  