---
description: 行為變更
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fb5501d362cb46f3616e58c5a4994bab86e00ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461620"
---
# <a name="behavioral-changes"></a>行為變更
行為變更是指介面的 *語法* 保持不變的變更，但 *語義* 已變更。 這些變更是 ODBC 2 中使用的功能。*x* 的行為與 ODBC 3 中的相同功能不同。*x*。  
  
 應用程式是否展示 ODBC 2。*x* 行為或 ODBC 3。*x* 行為是由 SQL_ATTR_ODBC_VERSION 環境屬性所決定。 這個32位值設定為 SQL_OV_ODBC2，以展現 ODBC 2。*x* 行為和 SQL_OV_ODBC3 展示 ODBC 3。*x* 行為。  
  
 SQL_ATTR_ODBC_VERSION 環境屬性是透過呼叫 **SQLSetEnvAttr**來設定。 當應用程式呼叫 **SQLAllocHandle** 來配置環境控制碼之後，它必須立即呼叫**SQLSetEnvAttr** 來設定它所展示的行為。  (的結果中，有一個新的環境狀態可描述已配置但無版本狀態中的環境控制碼。 ) 如需詳細資訊，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 應用程式會指出它在 SQL_ATTR_ODBC_VERSION 環境屬性中所呈現的行為，但屬性對 ODBC 2 的應用程式連接沒有任何作用。*x* 或 ODBC 3。*x* 驅動程式。 ODBC 3。*x* 應用程式可以連接到 ODBC 2。*x* 或3。*x* 驅動程式，不論環境屬性的設定為何。  
  
 ODBC 3。*x* 應用程式永遠不應該呼叫 **SQLAllocEnv**。 如此一來，如果驅動程式管理員接收到 **SQLAllocEnv**的呼叫，它就會將應用程式辨識為 ODBC 2。*x* 應用程式。  
  
 SQL_ATTR_ODBC_VERSION 屬性會影響 ODBC 3 的三個不同層面。*x* 驅動程式的行為：  
  
-   SQLSTATE  
  
-   日期、時間和時間戳記的資料類型  
  
-   **SQLTables**中的*CatalogName*引數接受 ODBC 3 中的搜尋模式。*x*，但不是在 ODBC 2 中。*x*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性的設定不會影響 **SQLSetParam** 或 **SQLBindParam**。 **SQLColAttribute** 也不會受到此位的影響。 雖然 **SQLColAttribute** 會傳回受 ODBC (日期類型、精確度、小數位數和長度) 影響的屬性，但預期的行為取決於 *FieldIdentifier* 引數的值。 當 *FieldIdentifier* 等於 SQL_DESC_TYPE 時， **SQLCOLATTRIBUTE** 會傳回 ODBC 3。日期、時間和時間戳記的*x* 代碼;當 *FieldIdentifier* 等於 SQL_COLUMN_TYPE 時， **SQLCOLATTRIBUTE** 會傳回 ODBC 2。日期、時間和時間戳記的*x* 代碼。  
  
 此章節包含下列主題。  
  
-   [SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
