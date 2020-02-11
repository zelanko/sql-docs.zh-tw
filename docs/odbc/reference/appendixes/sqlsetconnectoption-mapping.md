---
title: SQLSetConnectOption 對應 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b512a795c3b9e2d1c6aa1c7c9e92fbc42a8c7862
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125594"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 對應
當 ODBC 2。*x*應用程式會透過 ODBC*3.x 驅動程式*呼叫**SQLSetConnectOption** ，呼叫  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 將會產生如下所示：  
  
-   如果*fOption*表示 ODBC 定義的連接屬性需要字串，驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*表示 ODBC 定義的連接屬性，它會傳回32位的整數值，驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*表示驅動程式定義的連接屬性，則驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在上述三種情況中， *ConnectionHandle*引數會設定為*hdbc*中的值，而*屬性*引數會設定為*fOption*中的值，而*valueptr 是*引數會設定為與*vParam*相同的值。  
  
 因為驅動程式管理員不知道驅動程式定義的連接屬性是否需要字串或32位的整數值，所以必須針對**SQLSetConnectAttr**的*BufferLength*引數傳入有效值。 如果驅動程式已針對驅動程式定義的 connect 屬性定義特殊的語義，而且必須使用**SQLSetConnectOption**來呼叫它，則它必須支援**SQLSetConnectOption**。  
  
 如果是 ODBC 2。*x*應用程式會呼叫**SQLSETCONNECTOPTION** ，在 odbc*3.x 驅動程式*中設定驅動程式特定的語句選項，並在 odbc 2 中定義選項。*x*版的驅動程式，應該針對 ODBC*3.x 驅動程式*中的選項定義新的資訊清單常數。 如果在呼叫**SQLSetConnectOption**時使用舊的資訊清單常數，驅動程式管理員將會呼叫**SQLSetConnectAttr** ，並將**StringLength**引數設定為0。  
  
 對於 ODBC*3.x 驅動程式，驅動程式管理員*不會再檢查*fOption*是否介於 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX 之間，或是大於 SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>設定連接層級的語句選項  
 在 ODBC 2 中。*x*，應用程式可以呼叫**SQLSetConnectOption**來設定語句選項。 完成這項作業時，驅動程式會針對稍後為該連接配置的任何語句，建立語句選項做為預設值。 無論驅動程式是否針對與指定連接相關聯的任何現有語句，設定語句選項，都是驅動程式定義的。  
  
 這項功能已在 ODBC 3.x 中被*取代。* ODBC 3.x*驅動程式*只需要支援設定 odbc 2。連接層級的*x*語句屬性（如果它們想要使用 ODBC 2）。執行此動作的*x*應用程式。 ODBC 3.x*應用程式絕對*不應在連接層級設定語句屬性。 ODBC 3.x*語句屬性*無法在連接層級設定，但 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性（兩者都是連接屬性和語句屬性），而且可以在連接層級或語句層級設定。
