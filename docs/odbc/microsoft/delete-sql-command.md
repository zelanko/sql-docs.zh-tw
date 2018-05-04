---
title: 刪除 SQL 命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea0b09d77b6d2df8ddd525df17526573b6a1e1be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="delete---sql-command"></a>刪除 SQL 命令
將標示為刪除的記錄。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>引數  
 從 [ *DatabaseName ！*]*TableName*  
 指定的記錄標示為刪除的資料表。  
  
 *DatabaseName ！* 指定如果包含的資料庫不是與資料來源所指定的資料庫包含資料表的資料庫名稱。 您必須包含的資料庫，如果資料庫不是與資料來源所指定的資料庫包含之資料表的名稱。 在資料庫名稱之後和資料表名稱前面包含驚嘆號 （！） 分隔符號。  
  
 其中*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定 Visual FoxPro 標記為要刪除特定記錄。  
  
 *FilterCondition*指定記錄標示為刪除時必須符合的準則。 您可以包含篩選條件所要使用 AND 或 OR 運算子。 您也可以使用 NOT 運算子，若要反轉的邏輯運算式的值，或者您可以使用**空**（) 來檢查是否有空白的欄位。  
  
## <a name="remarks"></a>備註  
 如果設定刪除設為 ON，標示為刪除的記錄會忽略由包含範圍的所有命令。  
  
 刪除-SQL 的使用記錄鎖定的標記為要刪除資料表中的多筆記錄時開啟的共用存取。 這會減少記錄競爭情況，在多使用者情況下，但可能會降低效能。 最大效能，開啟專供資料表。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式刪除時，Visual FoxPro ODBC 驅動程式會將命令轉換到 Visual FoxPro 刪除命令，而不需轉譯。  
  
## <a name="see-also"></a>另請參閱  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
