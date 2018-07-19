---
title: 檢查資料的範例資料錄集 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a6bb3eb784c3979dd136f237c5d153547d30027
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272487"
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
