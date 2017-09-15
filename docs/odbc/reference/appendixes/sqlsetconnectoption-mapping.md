---
title: "SQLSetConnectOption 對應 |Microsoft 文件"
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
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e531888390bbe4f625d308ad983059634e84ba2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 對應
當 ODBC 2。*x*應用程式會呼叫**SQLSetConnectOption**透過 ODBC 3*.x*驅動程式，會呼叫  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 將會產生，如下所示：  
  
-   如果*fOption*指出需要字串時，驅動程式管理員呼叫 ODBC 定義的連接屬性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指出傳回 32 位元整數值，驅動程式管理員呼叫 ODBC 定義的連接屬性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*表示驅動程式定義的連接屬性，驅動程式管理員呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在前述三個情況下， *ConnectionHandle*引數設定中的值為*hdbc*、*屬性*引數設定中的值為*fOption*，而*ValuePtr*引數設定為相同的值做為*vParam*。  
  
 驅動程式管理員不知道驅動程式定義的連接屬性需要字串或 32 位元整數值，因為它必須傳入有效的值*Columnsize*引數的**SQLSetConnectAttr**. 如果驅動程式已定義特殊的語意的驅動程式定義連接屬性和需要使用呼叫**SQLSetConnectOption**，就必須支援**SQLSetConnectOption**。  
  
 如果 ODBC 2。*x*應用程式會呼叫**SQLSetConnectOption**設定驅動程式特有的陳述式選項，在 ODBC 3*.x*驅動程式，以及選擇定義在 ODBC 2。*x*版本的驅動程式時，新的資訊清單常數應該定義在 ODBC 3 選項*.x*驅動程式。 如果在呼叫中使用舊的資訊清單常數**SQLSetConnectOption**，驅動程式管理員會呼叫**SQLSetConnectAttr**與**StringLength**引數設定為 0。  
  
 ODBC 3*.x*驅動程式，驅動程式管理員不會再檢查，看看是否*fOption*之間 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX，或大於 SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>設定在連接層級上的陳述式選項  
 在 ODBC 2。*x*，應用程式可以呼叫**SQLSetConnectOption**設定陳述式選項。 完成時，驅動程式會建立做為預設值的陳述式選項的更新版本已配置該連接的任何陳述式。 它是驅動程式定義驅動程式是否設定與指定的連接相關聯的任何現有陳述式的陳述式選項。  
  
 這項功能已被取代，在 ODBC 3*.x*。 ODBC 3*.x*驅動程式只需要支援設定 ODBC 2。*x*陳述式屬性，在連接層級，如果他們想要使用的 ODBC 2。*x*執行這項操作的應用程式。 ODBC 3*.x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3*.x*陳述式屬性不能在連接層級，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 」 屬性，這些連接屬性和陳述式屬性，同時也可以設定在連接層級或陳述式層級設定。
