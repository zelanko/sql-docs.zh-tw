---
title: 處理定位更新與刪除語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308019"
---
# <a name="processing-positioned-update-and-delete-statements"></a>處理定點更新和刪除陳述式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 游標庫支援定位更新和刪除語句,將此類語句中的**WHERE CURRENT OF**子句替換為**WHERE**子句,該子句枚舉每個綁定列在其緩存中存儲的值。 游標庫將**新構造的更新**和**DELETE**語句傳遞給驅動程式以執行。 對於定位的更新語句,游標庫然後從行集緩衝區中的值更新其緩存,並將行狀態陣列中的相應值設置為SQL_ROW_UPDATED。 對於定位刪除語句,它將行狀態陣列中的相應值設置為SQL_ROW_DELETED。  
  
> [!CAUTION]  
>  游標庫為標識當前行而構造的**WHERE**子句可能無法標識任何行、標識其他行或標識多行。 有關詳細資訊,請參閱在此附錄的後面部分[建構搜尋語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 定位的更新與移除語句受以下限制:  
  
-   定位更新和刪除語句只能在以下情況下使用:當 SELECT 語句生成結果集時;**當 SELECT**語句生成結果集時,才能使用定位更新和刪除語句。當**SELECT**語句不包含聯接 **、UNION**子句或 GROUP **BY**子句時;以及當在選擇清單中使用別名或表達式的任何列未綁定**到 SQLBindCol**時。  
  
-   如果應用程式準備定位的更新或刪除語句,則必須在調用**SQLFetch**或**SQLFetchScroll**後執行此操作。 儘管遊標庫將語句提交到驅動程式進行準備,但它關閉語句並在應用程式調用**SQLExecute**時直接執行該語句。  
  
-   如果驅動程式僅支援一個活動語句,則游標庫將獲取結果集的其餘部分,然後在執行其定位的更新或刪除語句之前從緩存中重新提取當前行集。 如果應用程式然後調用一個函數,該函數返回結果集中的元資料(例如 **,SQLNumResultCols**或**SQLDescribeCol),** 則游標庫將傳回錯誤。  
  
-   如果在表的列上執行定位更新或刪除語句,該列包含每次執行更新時自動更新的時間戳列,則如果綁定時間戳列,則所有後續定位的更新或刪除語句都將失敗。 這是因為游標庫創建的搜索的更新或刪除語句無法準確標識要更新的行。 時間戳列的搜尋語句中的值與時間戳列的自動更新值不匹配。
