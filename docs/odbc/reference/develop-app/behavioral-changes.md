---
title: 行為變化 |微軟文件
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
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283438"
---
# <a name="behavioral-changes"></a>行為變更
行為更改是*介面語法保持不變*但*語義*已更改的更改。 對於這些更改,ODBC 2 中使用的功能。*x*的行為方式與 ODBC 3 中的相同功能不同。*x*. .  
  
 應用程式是否展示 ODBC 2。*x*行為或 ODBC 3。*x*行為由SQL_ATTR_ODBC_VERSION環境屬性決定。 此 32 位值設定為SQL_OV_ODBC2以顯示 ODBC 2。*x*行為,並SQL_OV_ODBC3展示ODBC 3。*x*行為。  
  
 SQL_ATTR_ODBC_VERSION環境屬性由對**SQLSetEnvAttr**的調用設置。 在應用程式調用**SQLAllocHandle**來分配環境句柄後,它必須立即調用**SQLSetEnv Attr**來設置它顯示的行為。 (因此,有一個新的環境狀態來描述在已分配但無版本狀態中的環境句柄。關於詳細資訊,請參閱附錄[B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 應用程式會指出它與SQL_ATTR_ODBC_VERSION環境屬性一起表現出的行為,但該屬性對應用程式與ODBC 2的連接沒有影響。*x*或 ODBC 3。*x*驅動程式。 ODBC 3.*x*應用程式可以連接到 ODBC 2。*x*或 3。*x*驅動程式,無論環境屬性設置如何。  
  
 ODBC 3.*x*應用程式絕不應呼叫**SQLAllocEnv**。 因此,如果驅動程式管理器收到對**SQLAllocEnv**的調用,它將應用程式識別為 ODBC 2。*x*應用程式。  
  
 SQL_ATTR_ODBC_VERSION屬性影響 ODBC 3 的三個不同方面。*x*驅動程式的行為:  
  
-   SQLSTATE  
  
-   日期、時間與時間戳的資料型態  
  
-   **SQLTables**中的*目錄名稱*參數接受 ODBC 3 中的搜尋模式。*x*,但不是在 ODBC 2 中。*x*  
  
 SQL_ATTR_ODBC_VERSION環境屬性的設定不會影響**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不受此位的影響。 儘管**SQLColAttribute**傳回受 ODBC 版本(日期類型、精度、比例和長度)影響的屬性,但預期行為由*FieldIdentifier*參數的值決定。 當*字段標識碼*等於SQL_DESC_TYPE時 **,SQLColAttribute**傳回 ODBC 3。*x*日期、時間和時間戳的代碼;當*字段標識碼*等於SQL_COLUMN_TYPE時 **,SQLColAttribute**傳回 ODBC 2。*x*日期、時間和時間戳的代碼。  
  
 此章節包含下列主題。  
  
-   [SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
