---
title: 行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc9f8dcc3782204c8bf1c9add1200e451edcf127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103869"
---
# <a name="behavioral-changes"></a>行為變更
行為變更會讓這些變更*語法*介面的維持不變，但*語意*已變更。 如需這些變更，ODBC 2 中所使用的功能。*x*行為不同於相同的功能，在 ODBC 3 行為。*x*。  
  
 不論應用程式表現 ODBC 2。*x*行為或 ODBC 3。*x*行為取決於 SQL_ATTR_ODBC_VERSION 環境屬性。 這個 32 位元值是設 SQL_OV_ODBC2 展現 ODBC 2。*x*行為，以及展現 ODBC 3 SQL_OV_ODBC3。*x*行為。  
  
 藉由呼叫設定了 SQL_ATTR_ODBC_VERSION 環境屬性**SQLSetEnvAttr**。 應用程式呼叫後**SQLAllocHandle**配置環境控制代碼，它必須呼叫**SQLSetEnvAttr**立即將它所表現的行為。 （如此一來，沒有新環境的狀態來描述環境控制代碼中配置，但 versionless，狀態）。如需詳細資訊，請參閱[附錄 b:狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 應用程式狀態以及它所表現的 SQL_ATTR_ODBC_VERSION [環境] 屬性，但該屬性的行為有 ODBC 2 應用程式的連接上沒有作用。*x*或 ODBC 3。*x*驅動程式。 ODBC 3。*x*應用程式可以連接至 ODBC 2。*x*或 3。*x*驅動程式，無論環境屬性的設定為何。  
  
 ODBC 3。*x*應用程式應該永遠不會呼叫**SQLAllocEnv**。 如此一來，如果驅動程式管理員會接收呼叫以**SQLAllocEnv**，它會辨識為 ODBC 2 應用程式。*x*應用程式。  
  
 SQL_ATTR_ODBC_VERSION 屬性會影響 ODBC 3 的三個不同的層面。*x*驅動程式的行為：  
  
-   SQLSTATE  
  
-   日期、 時間和時間戳記的資料類型  
  
-   *CatalogName*中的引數**SQLTables**接受搜尋模式，在 ODBC 3。*x*，而不是在 ODBC 2。*x*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性的設定不會影響**SQLSetParam**或是**SQLBindParam**。 **SQLColAttribute**也不會受到此位元。 雖然**SQLColAttribute**會傳回受影響的屬性 （date 類型、 有效位數、 小數位數和長度） 的 ODBC 版本，所預期的行為取決於值*FieldIdentifier*引數。 當*FieldIdentifier* SQL_DESC_TYPE、 相等**SQLColAttribute**會傳回 ODBC 3。*x*日期、 時間和時間戳記; 的程式碼時*FieldIdentifier* SQL_COLUMN_TYPE，等於**SQLColAttribute**傳回的 ODBC 2。*x*日期、 時間和時間戳記的程式碼。  
  
 此章節包含下列主題。  
  
-   [SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
