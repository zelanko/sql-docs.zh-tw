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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79a9c9a86e290f568f205a7e7678122f9089a7e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096336"
---
# <a name="delete---sql-command"></a>DELETE - SQL 命令
將標示為要刪除的記錄。  
  
 Visual FoxPro ODBC Driver 支援原生 Visual FoxPro 語言語法，此命令。 驅動程式專屬資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>引數  
 從 [ *DatabaseName ！* ]*TableName*  
 指定的記錄標示為刪除的資料表。  
  
 *DatabaseName ！* 指定如果包含的資料庫不是與資料來源所指定的資料庫包含資料表的資料庫名稱。 您必須包含的資料庫，如果資料庫不是與資料來源所指定的資料庫包含之資料表的名稱。 之後的資料庫名稱和資料表名稱之前，請包含驚嘆號 （！） 分隔符號。  
  
 何處*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定 Visual FoxPro 標記為要刪除特定記錄。  
  
 *FilterCondition*指定記錄標示為刪除時必須符合的準則。 您可以包含篩選條件所要連接 AND 或 OR 運算子。 您也可以使用 NOT 運算子來反轉邏輯運算式的值，或者您可以使用**空**（) 來檢查是否有空白的欄位。  
  
## <a name="remarks"></a>備註  
 如果設定刪除設為 ON，標示為要刪除的記錄會忽略包含某個範圍的所有命令。  
  
 刪除-SQL 的使用記錄鎖定在標記為要刪除資料表中的多筆記錄時開啟的共用存取。 這會減少記錄競爭情況，在多使用者的情況下，但可能會降低效能。 為達最佳效能，開啟獨佔使用的資料表。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式刪除時，則 Visual FoxPro ODBC Driver 會將命令轉換 Visual FoxPro 刪除命令，無需進行翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
