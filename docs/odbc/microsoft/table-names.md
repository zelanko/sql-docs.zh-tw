---
title: 表名稱 |微軟文件
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
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303119"
---
# <a name="table-names"></a>資料表名稱
當使用 dBASE、Microsoft Excel、Paradox 或文字驅動程式時,在「選擇」或「刪除」的 FROM 子句中、INSERT 中的 INTO 子句之後以及更新後、創建表和 DROP TABLE 中發生的表名稱可以包含有效的路徑、主名稱和檔名擴展名。  
  
 在 SQL 語句的其他位置使用表名稱不支援使用路徑或擴展,但僅接受主名稱(例如,EMP FROM FROM C:\ABC_EMP)。  
  
 可以使用關聯名稱(別名)。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
