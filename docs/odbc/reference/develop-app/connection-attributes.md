---
title: 連接屬性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0fad1db10e40c71d22dd75417420c54cefa7803
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194432"
---
# <a name="connection-attributes"></a>連接屬性
連接屬性是連接的特性。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣地，登入逾時或嘗試連接逾時之前, 等待的秒數是連接屬性。  
  
 設定連接屬性**SQLSetConnectAttr**和其目前的設定擷取**SQLGetConnectAttr**。 如果**SQLSetConnectAttr**之前呼叫驅動程式載入時，驅動程式管理員存放其連接結構中的屬性，並設定這些驅動程式中的連線程序的一部分。 不需要應用程式設定的任何連接屬性;所有的連接屬性都有預設值，其中有些是驅動程式特有。  
  
 連線，或其中一個，取決於屬性和驅動程式之前或之後，就可以設定連接屬性。 登入逾時 (SQL_ATTR_LOGIN_TIMEOUT) 套用至連線程序，且有效的只有當設定連接之前。 因為 ODBC 資料指標程式庫位於驅動程式管理員和驅動程式之間，必須連接之前，先設定的屬性，指定是否要使用 ODBC 資料指標程式庫 (SQL_ATTR_ODBC_CURSORS) 及 network packet size (SQL_ATTR_PACKET_SIZE) 和因此必須先載入此驅動程式之前。  
  
 若要指定資料來源是唯讀還是讀寫 (SQL_ATTR_ACCESS_MODE) 和目前的目錄 (SQL_ATTR_CURRENT_CATALOG) 可以設定之前或之後連接，取決於驅動程式屬性。 不過，互通的應用程式設定，這些連接之前因為有些驅動程式不支援變更這些連接之後。  
  
 有些連接屬性擁有預設值，才能建立連線，有些則不用。 這些會是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT，SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 連接之後，必須設定轉譯連接屬性 （SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION）。  
  
 所有其他連接屬性可以設定在任何時間。 如需詳細資訊，請參閱 < [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函式描述。 (連接屬性無法設定環境層級上，藉由呼叫**SQLSetEnvAttr**。)
