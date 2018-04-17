---
title: 陳述式選項 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ceeec4a042f2368701fa310ff62a52160b62ca38
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="statement-options"></a>陳述式選項
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項可讓自訂的應用程式內的特定執行陳述式。  
  
|陳述式選項|注意|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超過 2,147,483,647 個位元組或可用的記憶體。|  
|SQL_CONCURRENCY|允許的值，請參閱[資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驅動程式不允許 SQL_CURSOR_DYNAMIC。 請參閱[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)如需詳細資訊。 允許的值，請參閱[資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|傳回目前的記錄編號的書籤的 32 位元整數值。 取得; 僅限無法設定。|  
|SQL_KEYSET_SIZE|可以是只能設為 0。|  
|SQL_MAX_ROWS|若要從結果傳回的資料列數目上限設定。|  
|SQL_ROW_NUMBER|傳回 32 位元整數，指定目前的資料列結果集內的位置。 取得; 僅限無法設定。|  
|SQL_ROWSET_SIZE|不能超過 4,294,967,296 資料列。不過，您必須具有虛擬記憶體不足，無法在您的電腦，以處理您的要求。|  
|SQL_USE_BOOKMARKS|支援 SQL_USE_BOOKMARKS 設 SQL_UB_ON，並公開固定長度的書籤。|
