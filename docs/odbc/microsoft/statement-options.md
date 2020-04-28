---
title: 語句選項 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299208"
---
# <a name="statement-options"></a>陳述式選項
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 這些選項可讓您自訂應用程式內的特定執行語句。  
  
|語句選項|注意|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超過2147483647個位元組或可用的記憶體。|  
|SQL_CONCURRENCY|如需允許的值，請參閱資料[指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驅動程式不允許 SQL_CURSOR_DYNAMIC。 如需詳細資訊，請參閱[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 。 如需允許的值，請參閱資料[指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|傳回32位的整數值，這是目前記錄號碼的書簽。 僅取得;無法設定。|  
|SQL_KEYSET_SIZE|只能設定為0。|  
|SQL_MAX_ROWS|要從結果集傳回的最大資料列數目。|  
|SQL_ROW_NUMBER|傳回32位整數，指定結果集內目前資料列的位置。 僅取得;無法設定。|  
|SQL_ROWSET_SIZE|不能超過4294967296個數據列;不過，您的電腦上必須有足夠的虛擬記憶體，才能處理您的要求。|  
|SQL_USE_BOOKMARKS|支援將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON 並公開固定長度的書簽。|
