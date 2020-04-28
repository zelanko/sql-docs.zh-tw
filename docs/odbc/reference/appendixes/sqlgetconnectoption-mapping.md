---
title: SQLGetConnectOption 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d2905bd6793d032e485183c8f553cef2cdefda3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301999"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLGetConnectOption**時，呼叫  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 對應如下：  
  
-   如果*fOption*表示會傳回字串的 ODBC 定義連接選項，驅動程式管理員會呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*表示 ODBC 定義的連接選項，它會傳回32位的整數值，驅動程式管理員會呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*表示驅動程式定義的語句選項，驅動程式管理員會呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在上述三種情況中， *ConnectionHandle*引數會設定為*hdbc*中的值，而*屬性*引數會設定為*fOption*中的值，而*valueptr 是*引數會設定為與*pvParam*相同的值。  
  
 針對 ODBC 定義的字串連接選項，驅動程式管理員會將**SQLGetConnectAttr**呼叫中的*BufferLength*引數設定為預先定義的最大長度（SQL_MAX_OPTION_STRING_LENGTH）;若為非字串連接選項， *BufferLength*會設定為0。  
  
 對於 ODBC 3.x 驅動程式，*驅動程式管理員*不會再檢查 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX 之間是否有*選項*，或是大於 SQL_CONNECT_OPT_DRVR_START。 驅動程式必須檢查選項值的有效性。
