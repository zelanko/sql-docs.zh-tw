---
title: DELETE-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303549"
---
# <a name="delete---sql-command"></a>DELETE - SQL 命令
標示要刪除的記錄。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>引數  
 FROM [ *DatabaseName！*]*TableName*  
 指定記錄已標示為要刪除的資料表。  
  
 *名稱!* 如果包含的資料庫不是與資料來源一起指定的資料庫，則指定包含資料表的資料庫名稱。 如果資料庫不是使用資料來源所指定的資料庫，您就必須加入包含資料表的資料庫名稱。 在資料庫名稱後面和資料表名稱前面加上驚嘆號（！）分隔符號。  
  
 其中*FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 指定 Visual FoxPro 只標示要刪除的特定記錄。  
  
 *FilterCondition*指定記錄必須符合才能標示為刪除的準則。 您可以視需要包含多個篩選準則，並使用 AND 或 OR 運算子來連接它們。 您也可以使用 NOT 運算子來反轉邏輯運算式的值，也可以使用**empty**（）來檢查空白欄位。  
  
## <a name="remarks"></a>備註  
 如果 [設定已刪除] 設定為 [開啟]，則包含範圍的所有命令都會忽略標記為刪除的記錄。  
  
 DELETE-SQL 會在針對共用存取所開啟的資料表中標記多個要刪除的記錄時，使用記錄鎖定。 這可減少多使用者情況的記錄爭用，但可能會降低效能。 為了達到最大效能，請開啟資料表以供獨佔使用。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句 DELETE 傳送到資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成 Visual FoxPro DELETE 命令，而不會轉譯。  
  
## <a name="see-also"></a>另請參閱  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
