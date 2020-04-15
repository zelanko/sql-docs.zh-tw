---
title: 更新 - SQL 指令 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307639"
---
# <a name="update---sql-command"></a>UPDATE - SQL 命令
使用新值更新表中的記錄。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程式的資訊,請參閱**驅動程式備註**。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引數  
 更新 [*資料庫名稱1!**表格名稱1*  
 指定使用新值更新記錄的表。  
  
 *資料庫名稱1!* 指定資料庫的名稱,而不是使用包含表的數據來源指定的資料庫。 如果資料庫不是當前資料庫,則必須包含包含該表的資料庫的名稱。 包括資料庫名稱後和表名稱之前的感嘆號 (!) 分隔符。  
  
 設定*Column_Name1*= *eExpression1* * * = *,Column_Name2 *eExpression2*  
 指定更新的列及其新值。 如果省略 WHERE 子句,則列中的每一行都會使用相同的值進行更新。  
  
 其中*篩選準則1*[和&#124;或*過濾器條件2*...]  
 指定使用新值更新的記錄。  
  
 *篩選器條件*指定記錄必須滿足的條件才能使用新值進行更新。 您可以根據需要包含盡可能多的篩選條件,將它們與 AND 或 OR 運算元連接。 您還可以使用 NOT 運算子反轉邏輯表示式的值,也可以使用**EMPTY**( ) 檢查空欄位。  
  
## <a name="remarks"></a>備註  
 更新 - SQL 只能更新單個表中的記錄。  
  
 與 REPLACE 不同,UPDATE - SQL 在更新為共享存取的表中的多個記錄時使用記錄鎖定。 這減少了多使用者情況下的記錄爭用,但會降低性能。 為了達到最佳性能,打開表以專供獨佔使用,或使用**FLOCK**( ) 鎖定表。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句更新發送到數據源時,Visual FoxPro ODBC 驅動程式將該命令轉換為 Visual FoxProUPDATE 命令,無需翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [移除 - SQL 指令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
