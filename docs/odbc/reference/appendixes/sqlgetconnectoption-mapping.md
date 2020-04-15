---
title: SQLGetConnectOption 映射 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301999"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLGetConnectOption**時,呼叫  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 映射如下:  
  
-   如果*fOption*指示傳回字串的 ODBC 定義的連線選項,驅動程式管理員將呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示一個 ODBC 定義的連線選項,該選項傳回 32 位元整數值,則驅動程式管理員將呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驅動程式定義的語句選項,則驅動程式管理員將呼叫  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面三種情況下 *,ConnectHandle*參數設定為*hdbc*中的值,*屬性*參數設定為*fOption*中的值 *,ValuePtr*參數設定為與*pvParam*相同的值。  
  
 對於 ODBC 定義的字串連接選項,驅動程式管理器在調用**SQLGetConnectAttr**時將*緩衝區長度*參數設定為預定義的最大長度(SQL_MAX_OPTION_STRING_LENGTH);對於非字串連接選項,*緩衝區長度*設置為 0。  
  
 對於 ODBC *3.x*驅動程式,驅動程式管理器不再檢查*選項*是否位於SQL_CONN_OPT_MIN和SQL_CONN_OPT_MAX之間,還是大於SQL_CONNECT_OPT_DRVR_START。 驅動程式必須檢查選項值的有效性。
