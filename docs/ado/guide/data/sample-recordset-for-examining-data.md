---
description: 用於檢查資料的範例資料錄集
title: 用於檢查資料的範例記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: rothja
ms.author: jroth
ms.openlocfilehash: ec44c25bba9c792415c462e3028bbf20d8d3f84e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979739"
---
# <a name="sample-recordset-for-examining-data"></a>用於檢查資料的範例資料錄集
首先，讓我們看看使用下列 SQL 查詢所傳回的 **記錄集** 物件，它是針對 Microsoft SQL Server 中的 Northwind 範例資料基底所執行。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 結果 **集** 物件包含下表所示之資料庫中的所有產生。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|圖報 Bob 的有機蒙娜 Pears|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|Manjimup 蒙娜蘋果|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 如果您想要自行取得這些結果，請嘗試下列 JScript 範例：  
  
-   [傳回記錄集的 JScript 範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
