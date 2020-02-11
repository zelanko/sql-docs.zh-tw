---
title: 用於檢查資料的範例記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1882c5298d92e17a7ddaa165288fddfab7fdb02b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924301"
---
# <a name="sample-recordset-for-examining-data"></a>用於檢查資料的範例資料錄集
首先，讓我們使用下列 SQL 查詢（針對 Microsoft SQL Server 中的 Northwind 範例資料基底來執行），查看傳回的**記錄集**物件。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 結果**記錄集**物件包含資料庫中的所有產生，如下表所示。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|圖報 Bob 的有機蒙娜 Pears|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|Manjimup 蒙娜蘋果|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 如果您想要自行取得這些結果，請嘗試下列 JScript 範例：  
  
-   [傳回記錄集的 JScript 範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
