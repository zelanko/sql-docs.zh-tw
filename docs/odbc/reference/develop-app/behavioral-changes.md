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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103869"
---
# <a name="behavioral-changes"></a>行為變更
行為變更是介面*語法*保持不變的變更，但已變更此*語義*。 針對這些變更，ODBC 2 中使用的功能。*x*的行為與 ODBC 3 中的功能不同。*x*。  
  
 應用程式是否展現 ODBC 2。*x*行為或 ODBC 3。*x*行為是由 SQL_ATTR_ODBC_VERSION 環境屬性所決定。 這個32位值會設為 SQL_OV_ODBC2 以展示 ODBC 2。*x*行為和 SQL_OV_ODBC3 展示 ODBC 3。*x*行為。  
  
 SQL_ATTR_ODBC_VERSION 環境屬性是由呼叫**SQLSetEnvAttr**所設定。 在應用程式呼叫**SQLAllocHandle**來配置環境控制碼之後，它必須立即呼叫**SQLSetEnvAttr**來設定它所呈現的行為。 （如此一來，就有新的環境狀態可描述已配置但 versionless 的狀態中的環境控制碼）。如需詳細資訊，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 應用程式會指出它在 SQL_ATTR_ODBC_VERSION 環境屬性中所呈現的行為，但屬性不會影響 ODBC 2 的應用程式連接。*x*或 ODBC 3。*x*驅動程式。 ODBC 3。*x*應用程式可以連接到 ODBC 2。*x*或3。*x*驅動程式，不論環境屬性的設定為何。  
  
 ODBC 3。*x*應用程式應該永遠不會呼叫**SQLAllocEnv**。 因此，如果驅動程式管理員收到對**SQLAllocEnv**的呼叫，它會將應用程式辨識為 ODBC 2。*x*應用程式。  
  
 SQL_ATTR_ODBC_VERSION 屬性會影響 ODBC 3 的三個不同層面。*x*驅動程式的行為：  
  
-   SQLSTATE  
  
-   日期、時間和時間戳記的資料類型  
  
-   **SQLTables**中的*CatalogName*引數接受 ODBC 3 中的搜尋模式。*x*，但不在 ODBC 2 中。*x*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性的設定不會影響**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不會受到此位的影響。 雖然**SQLColAttribute**會傳回受 ODBC 版本（日期類型、有效位數、小數位數和長度）影響的屬性，但預期的行為是由*FieldIdentifier*引數的值所決定。 當*FieldIdentifier*等於 SQL_DESC_TYPE 時， **SQLCOLATTRIBUTE**會傳回 ODBC 3。日期、時間和時間戳記的*x*代碼;當*FieldIdentifier*等於 SQL_COLUMN_TYPE 時， **SQLCOLATTRIBUTE**會傳回 ODBC 2。日期、時間和時間戳記的*x*代碼。  
  
 此章節包含下列主題。  
  
-   [SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
