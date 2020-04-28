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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299039"
---
# <a name="connection-attributes"></a>連接屬性
連接屬性是連接的特性。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣地，登入超時，或在超時之前嘗試連接所等待的秒數，是連接屬性。  
  
 連接屬性會以**SQLSetConnectAttr**設定，而其目前設定會使用**SQLGetConnectAttr**來抓取。 如果在載入驅動程式之前呼叫**SQLSetConnectAttr** ，驅動程式管理員會將屬性儲存在其連接結構中，並將它們設定在驅動程式中，以做為連接過程的一部分。 應用程式不需要設定任何連接屬性;所有連接屬性都有預設值，其中有些是特定驅動程式。  
  
 連接屬性可以在連接前後設定，或視屬性和驅動程式而定。 登入超時（SQL_ATTR_LOGIN_TIMEOUT）會套用至連接程式，而且只有在連接之前設定時才有效。 指定是否要使用 ODBC 資料指標程式庫（SQL_ATTR_ODBC_CURSORS）和網路封包大小（SQL_ATTR_PACKET_SIZE）的屬性必須在連接之前設定，因為 ODBC 資料指標程式庫位於驅動程式管理員和驅動程式之間，因此必須在驅動程式之前載入。  
  
 屬性可指定資料來源為唯讀或讀寫（SQL_ATTR_ACCESS_MODE），而且可以在連接前後設定目前的目錄（SQL_ATTR_CURRENT_CATALOG），視驅動程式而定。 不過，互通的應用程式會在連接之前設定它們，因為某些驅動程式不支援在連接之後變更這些專案。  
  
 某些連接屬性在建立連線之前會有預設值，其他則不會。 其 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 連接之後，必須設定翻譯連接屬性（SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION）。  
  
 所有其他的連接屬性都可以隨時設定。 如需詳細資訊，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函數描述。 （無法藉由呼叫**SQLSetEnvAttr**在環境層級上設定連接屬性）。
