---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939781"
---
# <a name="table-names"></a>資料表名稱
當使用 dBASE、Microsoft Excel、Paradox 或文字驅動程式時，在 SELECT 或 DELETE 的 FROM 子句中發生的資料表名稱會在 INSERT 中的 INTO 子句之後，而且在 UPDATE、CREATE TABLE 和 DROP TABLE 之後可以包含有效的路徑、主要名稱和副檔名.  
  
 在 SQL 語句中的其他地方使用資料表名稱並不支援使用路徑或延伸，但只會接受主要名稱（例如，從 C:\ABC\EMP EMP）。  
  
 您可以使用相互關聯名稱（別名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
