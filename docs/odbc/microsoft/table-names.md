---
description: 資料表名稱
title: 資料表名稱 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b264999f800e4387099240526f558110c39e27a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471456"
---
# <a name="table-names"></a>資料表名稱
使用 dBASE、Microsoft Excel、Paradox 或 Text 驅動程式時，在 SELECT 或 DELETE 的 FROM 子句中出現的資料表名稱、INSERT 中的 INTO 子句之後，以及更新之後、CREATE TABLE 和 DROP TABLE 可以包含有效的路徑、主要名稱和副檔名。  
  
 在 SQL 語句中的其他位置使用資料表名稱並不支援使用路徑或延伸模組，但只會接受主要名稱 (例如，從 C:\ABC\EMP) EMP。  
  
 您可以使用)  (別名的相互關聯名稱。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
