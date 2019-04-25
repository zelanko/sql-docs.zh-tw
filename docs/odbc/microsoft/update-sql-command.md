---
title: UPDATE-SQL 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbd5ec98791d782fe7ad1fdb1e1884b646dcf9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632555"
---
# <a name="update---sql-command"></a>UPDATE - SQL 命令
使用新值更新資料表中的記錄。  
  
 Visual FoxPro ODBC Driver 支援原生 Visual FoxPro 語言語法，此命令。 驅動程式專屬資訊，請參閱**驅動程式備註**。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引數  
 UPDATE [ *DatabaseName1!*] *TableName1*  
 指定的新值更新記錄的資料表。  
  
 *DatabaseName1!* 指定包含資料表的資料來源所指定的資料庫以外的資料庫名稱。 您必須包括包含的資料表，如果資料庫不是目前資料庫的名稱。 之後的資料庫名稱和資料表名稱之前，請包含驚嘆號 （！） 分隔符號。  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 指定更新的資料行和其新的值。 如果您省略 WHERE 子句，資料行中的每個資料列會更新以相同的值。  
  
 何處*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定的記錄，則會以新值更新。  
  
 *FilterCondition*指定記錄必須符合使用新的值進行更新的準則。 例如，連接及篩選條件，您可以包含或 OR 運算子。 您也可以使用 NOT 運算子來反轉邏輯運算式的值，或者您可以使用**空**（) 來檢查是否有空白的欄位。  
  
## <a name="remarks"></a>備註  
 更新-SQL 可以更新只會在單一資料表中的記錄。  
  
 不同於取代更新-SQL 會使用記錄鎖定更新資料表中的多筆記錄開啟的共用存取時。 這會減少記錄競爭情況，在多使用者的情況下，但可能會降低效能。 達到最佳效能，請開啟資料表的獨佔使用，或使用**FLOCK**（) 來鎖定資料表。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式更新時，則 Visual FoxPro ODBC Driver 會將命令轉換 Visual FoxProUPDATE 命令，無需進行翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE-SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
