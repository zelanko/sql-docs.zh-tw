---
title: 啟用追蹤 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287348"
---
# <a name="enabling-tracing"></a>啟用追蹤
您可以透過下列三種方式來啟用追蹤：  
  
-   在 Odbc .ini 登錄專案中設定**Trace**和**TraceFile**關鍵字。 這會在呼叫**SQLAllocHandle**時，啟用或停用*HandleType*為 SQL_HANDLE_ENV 的追蹤。 這些選項是在資料來源設定期間顯示的 [ODBC 資料來源管理員] 對話方塊的 [追蹤] 索引標籤中設定。 如需詳細資訊，請參閱[資料來源的登錄專案](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   呼叫**SQLSetConnectAttr** ，將 SQL_ATTR_TRACE 連接屬性設定為 SQL_OPT_TRACE_ON。 這會啟用或停用連接期間的追蹤。 如需詳細資訊，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函數描述。  
  
-   使用**ODBCSharedTraceFlag** ，以動態方式開啟或關閉追蹤。 （如需詳細資訊，請參閱下一個主題：[動態追蹤](../../../odbc/reference/develop-app/dynamic-tracing.md)）。
