---
title: 語句選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299208"
---
# <a name="statement-options"></a>陳述式選項
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項允許在應用程式中自定義特定的執行語句。  
  
|語句選項|注意|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超過 2,147,483,647 位元組或可用記憶體。|  
|SQL_CONCURRENCY|有關允許的值,請參閱[游標類型和併發組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驅動程式不允許SQL_CURSOR_DYNAMIC。 關於詳細資訊[,請參閱 SQLSetScroll 選項](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)。 有關允許的值,請參閱[游標類型和併發組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|返回作為當前記錄編號的書籤的 32 位整數值。 只獲取;無法設置。|  
|SQL_KEYSET_SIZE|只能設置為 0。|  
|SQL_MAX_ROWS|要從結果集中返回的最大行數。|  
|SQL_ROW_NUMBER|返回一個 32 位整數,指定結果集中當前行的位置。 只獲取;無法設置。|  
|SQL_ROWSET_SIZE|不能超過 4,294,967,296 行;但是,您的電腦中必須有足夠的虛擬記憶體來處理您的請求。|  
|SQL_USE_BOOKMARKS|支援將SQL_USE_BOOKMARKS設置為SQL_UB_ON並公開固定長度的書籤。|
