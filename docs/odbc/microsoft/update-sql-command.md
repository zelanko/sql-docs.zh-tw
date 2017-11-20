---
title: "更新-SQL 命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4aaf4c9d8e44108888c2c440fba506cf9b2874c8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="update---sql-command"></a>更新-SQL 命令
新值來更新資料表中的記錄。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱**驅動程式註解**。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引數  
 更新 [ *DatabaseName1 ！*]*TableName1*  
 指定的新值更新記錄的資料表。  
  
 *DatabaseName1 ！* 指定包含資料表的資料來源所指定的資料庫以外的資料庫名稱。 您必須包括包含的資料表，如果資料庫不是目前資料庫的名稱。 在資料庫名稱之後和資料表名稱前面包含驚嘆號 （！） 分隔符號。  
  
 設定*Column_Name1*= *eExpression1*[， *Column_Name2*= *eExpression2*  
 指定更新的資料行和新的值。 如果您省略 WHERE 子句，資料行中的每個資料列會更新以相同的值。  
  
 其中*FilterCondition1*[AND &#124;或者*FilterCondition2*...]  
 指定更新新值的記錄。  
  
 *FilterCondition*指定記錄更新為新的值必須符合的準則。 您可以包含任意，使用 AND 篩選條件或 OR 運算子。 您也可以使用 NOT 運算子，若要反轉的邏輯運算式的值，或者您可以使用**空**（) 來檢查是否有空白的欄位。  
  
## <a name="remarks"></a>備註  
 更新-SQL 可以更新只能在單一資料表的記錄。  
  
 不同於取代，更新-SQL 會使用記錄鎖定更新資料表中的多筆記錄開啟的共用存取時。 這會減少記錄競爭情況，在多使用者情況下，但可能會降低效能。 最大效能，請開啟資料表的獨佔使用，或使用**FLOCK**（) 來鎖定資料表。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式會將 ODBC SQL 陳述式更新傳送至資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成 Visual FoxProUPDATE 命令，而不需轉譯中。  
  
## <a name="see-also"></a>另請參閱  
 [刪除 SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [插入的 SQL 命令](../../odbc/microsoft/insert-sql-command.md)

