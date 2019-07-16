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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939781"
---
# <a name="table-names"></a>資料表名稱
DBASE、 Microsoft Excel、 Paradox，或使用驅動程式的文字、 資料表名稱中所發生的 SELECT 或 DELETE FROM 子句之後在 INSERT INTO 子句，並更新之後，CREATE TABLE 和 DROP TABLE 可包含有效的路徑、 主要名稱和檔案名稱時延伸模組.  
  
 使用 SQL 陳述式中的其他位置的資料表名稱不支援的路徑或延伸模組使用，但接受只有主要名稱 (例如，EMP 從 C:\ABC\EMP)。  
  
 可以使用相互關聯名稱 （別名）。 例如:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
