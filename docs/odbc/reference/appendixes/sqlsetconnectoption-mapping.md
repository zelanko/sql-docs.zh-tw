---
description: SQLSetConnectOption 對應
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c1f1379bfd2bbc2faccf719d68009ed63b350fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476960"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 對應
當 ODBC 2 時。*x* *應用程式透過 ODBC 3.x 驅動程式*呼叫**SQLSetConnectOption** ，呼叫  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 將會產生如下的結果：  
  
-   如果 *fOption* 指出需要字串的 ODBC 定義連接屬性，驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果 *fOption* 指出 ODBC 定義的連接屬性，而此屬性會傳回32位整數值，驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果 *fOption* 指出驅動程式定義的連接屬性，驅動程式管理員會呼叫  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在上述三種情況下， *ConnectionHandle* 引數會設定為 *hdbc*中的值、 *屬性* 引數設定為 *fOption*中的值，而 *ValuePtr* 引數則設定為與 *vParam*相同的值。  
  
 因為驅動程式管理員不知道驅動程式定義的連接屬性是否需要字串或32位整數值，所以必須針對**SQLSetConnectAttr**的*BufferLength*引數傳入有效的值。 如果驅動程式已為驅動程式定義的連接屬性定義特殊的語法，且需要使用 **SQLSetConnectOption**來呼叫，則必須支援 **SQLSetConnectOption**。  
  
 如果是 ODBC 2。*x* 應用程式會呼叫 **SQLSetConnectOption** ，以在 odbc*3.x 驅動程式* 中設定驅動程式特定的語句選項，而此選項定義于 odbc 2 中。*x* 版本的驅動程式，則應該為 ODBC*3.x 驅動程式* 中的選項定義新的資訊清單常數。 如果在 **SQLSetConnectOption**的呼叫中使用舊的資訊清單常數，驅動程式管理員會呼叫 **SQLSetConnectAttr** ，並將 **StringLength** 引數設定為0。  
  
 針對 ODBC*3.x 驅動程式，驅動程式管理員* 不會再檢查 *fOption* 是否在 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX 之間，或是大於 SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>在連接層級上設定語句選項  
 在 ODBC 2 中。*x*，應用程式可以呼叫 **SQLSetConnectOption** 來設定語句選項。 完成時，驅動程式會將語句選項建立為稍後針對該連接配置的任何語句的預設值。 它是驅動程式定義的，不論驅動程式是否為與指定連接相關聯的任何現有語句設定語句選項。  
  
 這項功能已在 ODBC 3.x 中被*取代。* ODBC 3.x*驅動程式* 只需要支援設定 ODBC 2。連接層級的*x* 語句屬性（如果想要使用 ODBC 2 的話）。這樣做的*x* 應用程式。 ODBC 3.x*應用程式* 絕對不應該在連接層級設定語句屬性。 ODBC 3.x*語句屬性* 無法在連接層級設定，但 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性（兩者都是連接屬性和語句屬性）除外，而且可以在連接層級或語句層級設定。
