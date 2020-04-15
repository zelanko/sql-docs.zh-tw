---
title: 確定游標功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305879"
---
# <a name="determining-cursor-capabilities"></a>判斷資料指標的功能
**SQLGetInfo**中的以下四個選項描述了支援哪些類型的游標及其功能:  
  
-   SQL_CURSOR_SENSITIVITY 指示游標是否對另一個游標所做的更改敏感。  
  
-   SQL_SCROLL_OPTIONS 列出支援的游標類型(僅轉發、靜態、鍵集驅動、動態或混合)。 所有數據源都必須支援僅轉發游標。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1(取決於游標的類型)。 列出可滾動遊標支援的提取類型。 返回值中的位對應於**SQLFetchScroll**中的提取類型。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2或SQL_STATIC_CURSOR_ATTRIBUTES2(取決於游標的類型)。 列出靜態和按鍵集驅動的遊標是否可以檢測自己的更新、刪除和插入。  
  
 應用程式可以通過使用這些選項調用**SQLGetInfo**來確定運行時的游標功能。 這通常由通用應用程式完成。 游標功能也可以在應用程式開發期間確定,並在應用程式中硬編碼使用。 這通常由垂直和自定義應用程式完成,但也可以通過使用客戶端游標實現的泛型應用程式(如 ODBC 游標庫)來完成。
