---
title: "檢查資料的範例資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: edc5419a18d658d9a0e10dc40b69ceb41c730bd4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sample-recordset-for-examining-data"></a>檢查資料的範例資料錄集
首先，讓我們看看**資料錄集**使用執行針對 Northwind 範例資料的 Microsoft SQL Server 中的基底的下列 SQL 查詢傳回的物件。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 產生**資料錄集**物件包含下表顯示資料庫中的所有產生。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|得以 Bob 有機曬的梨子|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|馬普乾蘋果|53.0000|  
|74|長壽豆腐|10.0000|  
  
 如果您有興趣自行取得這些結果，請嘗試下列 JScript 範例：  
  
-   [傳回一個資料錄集的 JScript 範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)

