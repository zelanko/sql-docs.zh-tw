---
title: "啟用追蹤 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d80f7e70915c11a3a45f90d2821b9c1bd137d9dd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-tracing"></a>啟用追蹤
追蹤可啟用下列三種方式：  
  
-   設定**追蹤**和**TraceFile** Odbc.ini 登錄項目中的關鍵字。 這啟用或停用追蹤時**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_ENV 的呼叫。 ODBC 資料來源管理員] 對話方塊的 [資料來源的安裝過程中顯示 [追蹤] 索引標籤中設定這些選項。 如需詳細資訊，請參閱[資料來源的登錄項目](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   呼叫**SQLSetConnectAttr**設 SQL_OPT_TRACE_ON SQL_ATTR_TRACE 連接屬性。 這可以啟用或停用連線的持續時間的追蹤。 如需詳細資訊，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函式描述。  
  
-   使用**ODBCSharedTraceFlag**若要開啟或關閉追蹤以動態方式。 (如需詳細資訊，請參閱下一個主題[動態追蹤](../../../odbc/reference/develop-app/dynamic-tracing.md)。)

