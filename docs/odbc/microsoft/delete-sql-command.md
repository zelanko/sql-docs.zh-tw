---
title: 刪除 - SQL 指令 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303549"
---
# <a name="delete---sql-command"></a>DELETE - SQL 命令
標記記錄以進行刪除。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程序的資訊,請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>引數  
 從資料庫*名稱!**表格名稱*  
 指定在其中標記記錄以進行刪除的表。  
  
 *資料庫名稱!* 指定包含表的資料庫的名稱,如果包含的資料庫不是使用數據來源指定的資料庫。 如果資料庫不是使用數據源指定的資料庫,則必須包含包含表的資料庫的名稱。 包括資料庫名稱後和表名稱之前的感嘆號 (!) 分隔符。  
  
 其中*篩選準則1*[和&#124;或*過濾器條件2*...]  
 指定 Visual FoxPro 僅標記某些記錄以進行刪除。  
  
 *篩選器條件*指定記錄必須滿足的條件才能標記為刪除。 您可以根據需要包含盡可能多的篩選器條件,將它們與 AND 或 OR 運算元連接。 您還可以使用 NOT 運算子反轉邏輯表示式的值,也可以使用**EMPTY**( ) 檢查空欄位。  
  
## <a name="remarks"></a>備註  
 如果 SET DELETED 設定為「打開」,則標記為刪除的記錄將被包含作用域的所有命令忽略。  
  
 刪除 - SQL 在標記多個記錄以在打開的用於共用訪問的表中刪除時使用記錄鎖定。 這減少了多使用者情況下的記錄爭用,但會降低性能。 為了達到最佳性能,打開表以專供獨佔使用。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句 DELETE 發送到資料來源時,Visual FoxPro ODBC 驅動程式將該命令轉換為 Visual FoxPro DELETE 命令,無需翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
