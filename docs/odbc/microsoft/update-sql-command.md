---
title: 更新-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307639"
---
# <a name="update---sql-command"></a>UPDATE - SQL 命令
以新值更新資料表中的記錄。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱**驅動程式備註**。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引數  
 更新 [ *DatabaseName1！*]*TableName1*  
 指定以新值更新記錄的資料表。  
  
 *DatabaseName1!* 指定資料庫的名稱，而不是使用包含資料表的資料來源所指定的資料庫。 如果資料庫不是最新的，您必須包含包含資料表的資料庫名稱。 在資料庫名稱後面和資料表名稱前面加上驚嘆號（！）分隔符號。  
  
 SET *Column_Name1*= *eExpression1*[， *Column_Name2*= *eExpression2*  
 指定已更新的資料行及其新值。 如果您省略 WHERE 子句，資料行中的每個資料列都會更新為相同的值。  
  
 其中*FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 指定以新值更新的記錄。  
  
 *FilterCondition*指定記錄必須符合才能以新值更新的準則。 您可以視需要包含多個篩選準則，並使用 AND 或 OR 運算子來連接它們。 您也可以使用 NOT 運算子來反轉邏輯運算式的值，也可以使用**empty**（）來檢查空白欄位。  
  
## <a name="remarks"></a>備註  
 UPDATE-SQL 只能更新單一資料表中的記錄。  
  
 不同于 REPLACE，更新-SQL 會在針對共用存取所開啟的資料表中更新多筆記錄時，使用記錄鎖定。 這可減少多使用者情況的記錄爭用，但可能會降低效能。 為了達到最大效能，請開啟資料表以供獨佔使用，或使用**FLOCK**（）來鎖定資料表。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句更新傳送至資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成 Visual FoxProUPDATE 命令，而不會轉譯。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE-SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
