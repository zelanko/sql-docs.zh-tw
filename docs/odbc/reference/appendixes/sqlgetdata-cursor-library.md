---
title: SQLGet數據(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307839"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLGetData**函數。 有關**SQLGetData**的一般資訊,請參閱[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 游標庫通過首先建構一個**SELECT**語句來實現**SQLGetData,** 該語句具有**WHERE**子句,該子句枚舉當前行中每個綁定列存儲在其緩存中的值。 然後,它執行**SELECT**語句以重新選擇該行,並在驅動程式中調用**SQLGetData**以從資料來源(而不是緩存)檢索數據。  
  
> [!CAUTION]  
>  游標庫為標識當前行而構造的**WHERE**子句可能無法標識任何行、標識其他行或標識多行。 有關詳細資訊,請參閱[建構搜尋語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果將SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,則可以在第 0 列上調用**SQLGetData**來返回書籤數據。  
  
 對**SQLGetData 的**呼叫限制限制:  
  
-   不能為僅轉發游標調用**SQLGetData。**  
  
-   僅當滿足以下條件時才能調用**SQLGetData:SELECT****SELECT**語句 生成結果集;**SELECT**語句不包含聯接 **、UNION**子句或**GROUP BY**子句;並且在選擇清單中使用別名或表示式的任何列未綁定到**SQLBindCol**。  
  
-   如果驅動程式僅支援一個活動語句,則游標庫在執行**SELECT**語句並調用**SQLGetData**之前獲取結果集的其餘部分。
