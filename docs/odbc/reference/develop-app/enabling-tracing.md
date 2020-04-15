---
title: 開啟追蹤 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287348"
---
# <a name="enabling-tracing"></a>啟用追蹤
可使用以下三種方式開啟追蹤:  
  
-   在 Odbc.ini 註冊表條目中設定**追蹤**和**追蹤檔**關鍵字。 當調用具有*SQL_HANDLE_ENV的* **SQLAllocHandle**時,這將啟用或禁用跟蹤。 這些選項設置在資料來源設定期間顯示的 ODBC 資料來源管理員對話方塊的「追蹤」選項卡中。 有關詳細資訊,請參閱[資料來源的註冊表項](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   調用**SQLSetConnect Attr**將SQL_ATTR_TRACE連接屬性設置為SQL_OPT_TRACE_ON。 這將啟用或禁用連接持續時間的跟蹤。 有關詳細資訊,請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函數說明。  
  
-   使用**ODBC 共用追蹤 Flag**動態打開或關閉追蹤。 (有關詳細資訊,請參閱下一個主題["動態跟蹤](../../../odbc/reference/develop-app/dynamic-tracing.md)"。)
