---
title: "行為變更 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ccd4cdd57771d32a6a09bf1c1030ba173ee18486
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="behavioral-changes"></a>行為變更
行為變更會這些變更*語法*介面的維持不變，但*語意*已變更。 如需這些變更，ODBC 2 中使用的功能。*x*行為不同於相同的功能，在 ODBC 3 行為。*x*。  
  
 應用程式是否會表現 ODBC 2。*x*行為或 ODBC 3。*x*行為取決於 SQL_ATTR_ODBC_VERSION 環境屬性。 這個 32 位元值設定為 SQL_OV_ODBC2 至展現 ODBC 2。*x*行為，以及至展現 ODBC 3 SQL_OV_ODBC3。*x*行為。  
  
 藉由呼叫設定了 SQL_ATTR_ODBC_VERSION 環境屬性**SQLSetEnvAttr**。 應用程式呼叫之後**SQLAllocHandle**配置環境控制代碼，它必須呼叫**SQLSetEnvAttr**立即將它所表現的行為。 （如此一來，沒有新環境的狀態來描述環境控制代碼中已配置，但 versionless，狀態。）如需詳細資訊，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 應用程式狀態以及它 SQL_ATTR_ODBC_VERSION 環境屬性，但屬性所表現的行為有應用程式的 ODBC 2 連接上沒有作用。*x*或 ODBC 3。*x*驅動程式。 ODBC 3。*x*應用程式可以連接至 ODBC 2。*x*或 3。*x*驅動程式，不論環境屬性的設定為何。  
  
 ODBC 3。*x*應用程式應該永遠不會呼叫**SQLAllocEnv**。 如此一來，如果驅動程式管理員會接收呼叫**SQLAllocEnv**，它會辨識應用程式為 ODBC 2。*x*應用程式。  
  
 SQL_ATTR_ODBC_VERSION 屬性會影響 ODBC 3 的三個不同的層面。*x*驅動程式的行為：  
  
-   SQLSTATE  
  
-   針對日期、 時間和時間戳記資料類型  
  
-   *CatalogName*引數中的**SQLTables**接受 ODBC 3 中的搜尋模式。*x*，但不是在 ODBC 2。*x*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性的設定不會影響**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不會受到此位元。 雖然**SQLColAttribute**傳回受影響的屬性 （date 類型、 有效位數、 小數位數和長度） 的 ODBC 版本，所預期的行為取決於值*FieldIdentifier*引數。 當*FieldIdentifier*等於的 SQL_DESC_TYPE、 **SQLColAttribute**傳回 ODBC 3。*x*日期、 時間和時間戳記，程式碼時*FieldIdentifier*等於 SQL_COLUMN_TYPE， **SQLColAttribute**傳回 ODBC 2。*x*日期、 時間和時間戳記的代碼。  
  
 此章節包含下列主題。  
  
-   [SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
