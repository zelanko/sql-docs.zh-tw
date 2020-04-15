---
title: SQLSetConnectOption 映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287468"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 對應
當一個ODBC 2。*x*應用程式透過 ODBC 3 *.x*驅動程式呼叫**SQLSetConnectOption,** 呼叫  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 結果如下:  
  
-   如果*fOption*指示需要字串的 ODBC 定義的連線屬性,驅動程式管理員將呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示傳回 32 位元整數值的 ODBC 定義的連線屬性,則驅動程式管理員將呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驅動程式定義的連線屬性,則驅動程式管理員將呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在前面三種情況下 *,ConnectHandle*參數設定為*hdbc*中的值,*屬性*參數設定為*fOption*中的值 *,ValuePtr*參數設定為與*vParam*相同的值。  
  
 由於驅動程式管理員不知道驅動程式定義的連接屬性是否需要字串還是 32 位元整數值,因此必須為**SQLSetConnectAttr**的*BufferLength*參數傳遞有效值。 如果驅動程式為驅動程式定義的連線屬性定義了特殊語義,並且需要使用**SQLSetConnectOption**呼叫 ,則必須支援**SQLSetConnectOption**。  
  
 如果 ODBC 2.*x*應用程式呼叫**SQLSetConnectOption**在 ODBC 3 *.x*驅動程式中設定特定於驅動程式的語句選項,該選項在 ODBC 2 中定義。*驅動程式*的 x 版本,應為 ODBC 3 *.x*驅動程式中的選項定義新的清單常量。 如果在調用**SQLSetConnectOption**時使用舊的清單常量,驅動程式管理器將調用**SQLSetConnectAttr,****字串長度**參數設定為 0。  
  
 對於 ODBC 3 *.x*驅動程式,驅動程式管理器不再檢查*fOption*是否位於SQL_CONN_OPT_MIN和SQL_CONN_OPT_MAX之間,還是大於SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>在連接層級設定文句選項  
 在 ODBC 2 中。*x*,應用程式可以調用**SQLSetConnectOption**來設置語句選項。 完成此操作後,驅動程式將語句選項作為以後為該連接分配的任何語句的預設值。 驅動程式是否為與指定連接關聯的任何現有語句設置語句選項,由驅動程式定義。  
  
 此能力已在 ODBC 3 *.x*中被棄用。 ODBC 3 *.x*驅動程式只需要支援設定 ODBC 2。*x*語句屬性在連接級別,如果他們想與 ODBC 2 一起工作。*x*執行此操作的應用程式。 ODBC 3 *.x*應用程式絕不應在連接級別設置語句屬性。 ODBC 3 *.x*語句屬性無法在連接級別設置,但SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE屬性除外,這些屬性既是連接屬性,也是語句屬性,可以在連接級別或語句級別進行設置。
