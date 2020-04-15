---
title: 目錄資料的使用 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306809"
---
# <a name="uses-of-catalog-data"></a>使用目錄資料
應用程式以各種方式使用目錄數據。 下面是一些常見的用途:  
  
-   **在運行時構造 SQL 語句。** 垂直應用程式(如訂單輸入應用程式)包含硬編碼的 SQL 語句。 應用程式使用的表和列提前修復,訪問這些表的語句也提前修復。 例如,訂單輸入應用程式通常包含單個參數化**的INSERT**語句,用於向系統添加新訂單。  
  
     通用應用程式(如使用 ODBC 檢索資料的電子表格程式)通常根據使用者輸入在運行時建構 SQL 語句。 此類應用程式可能要求使用者鍵入要使用的表和列的名稱。 但是,如果應用程式顯示使用者可以從中進行選擇的表和列的清單,則使用者會更容易。 要生成這些清單,應用程式將調用**SQLTables**和**SQLColumns**目錄函數。  
  
-   **在開發過程中構造 SQL 語句。** 應用程式開發環境通常允許程式師在開發程式時創建資料庫查詢。 然後,在正在生成的應用程式中對查詢進行硬編碼。  
  
     此類環境還可以使用**SQLTables**和**SQLColumns**創建程式師可以從中進行選擇的清單。 這些環境還可能使用**SQLPrimaryKeys**和**SQL 外鍵**自動確定和顯示所選表之間的關係,並使用**SQLStatistics**來確定和突出顯示索引欄位,以便程式師可以創建高效的查詢。  
  
-   **構造遊標。** 提供可滾動遊標引擎的應用程式、驅動程式或中間件可以使用**SQL 特別列**來確定哪個列或列唯一標識一行。 程式可以生成一個*鍵集*,其中包含已提取的每行的這些列的值。 當應用程式滾動回行時,它將使用這些值獲取該行的最新數據。 有關可滾動遊標和鍵集的詳細資訊,請參閱[可捲動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。
