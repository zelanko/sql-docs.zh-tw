---
title: 執行定位更新與刪除語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306999"
---
# <a name="executing-positioned-update-and-delete-statements"></a>執行定點更新和刪除陳述式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 應用程式使用**SQLFetchScroll**獲取數據塊後,可以更新或刪除區塊中的資料。 要執行定位的更新或移除, 應用程式:  
  
1.  呼叫**SQLSetPos**將游標放置在要更新或刪除的行上。  
  
2.  使用以下語法建構定位的更新或移除語句:  
  
     **更新***表格名稱*  
  
     **設定***欄識別碼***=**= &#124; **NULL**的*表示式*|  
  
     【**,***列識別子***=**】*表示式*&#124; **NULL**]  
  
     **其中***游標名稱的*目前  
  
     **從***表格名稱移除**游標名稱***的目前**位置  
  
     在定位更新語句中建構**SET**子句的最簡單方法是對要更新的每個列使用參數標記,並使用**SQLBind 參數**將這些參數綁定到要更新行的行集緩衝區。 在這種情況下,參數的 C 數據類型將與行集緩衝區的 C 數據類型相同。  
  
3.  如果當前行將執行定位的更新語句,則更新當前行的行集緩衝區。 成功執行定位的更新語句后,游標庫將當前行中每列的值複製到其緩存。  
  
    > [!CAUTION]  
    >  如果應用程式在執行定位的更新語句之前未正確更新行集緩衝區,則在執行語句后,緩存中的數據將不正確。  
  
4.  使用與游標關聯的語句不同的語句執行定位的更新或刪除語句。  
  
    > [!CAUTION]  
    >  游標庫為標識當前行而構造的**WHERE**子句可能無法標識任何行、標識其他行或標識多行。 有關詳細資訊,請參閱[建構搜尋語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位的更新和刪除語句都需要游標名稱。 要指定游標名稱,應用程式在打開游標之前調用**SQLSetCursorName。** 要使用驅動程式生成的游標名稱,應用程式在打開游標後調用**SQLGetCursorName。**  
  
 游標庫執行定位的更新或刪除語句后,游標庫維護的狀態陣列、行集緩衝區和緩存包含下表中顯示的值。  
  
|使用敘述|列狀態陣列中的值|中的值<br /><br /> 排集緩衝區|中的值<br /><br /> 快取緩衝區|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定點更新|SQL_ROW_UPDATED|新值[1]|新值[1]|  
|請找到刪除|SQL_ROW_DELETED|舊值|舊值|  
  
 [1] 應用程式在執行定位的更新語句之前必須更新行集緩衝區中的值;執行定位的更新語句后,游標庫將行集緩衝區中的值複製到其緩存。
