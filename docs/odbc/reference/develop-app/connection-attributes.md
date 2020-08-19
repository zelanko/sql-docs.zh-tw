---
description: 連接屬性
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
ms.openlocfilehash: a7db2fb6361f114f4864436116f5b0f2f5651e79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424800"
---
# <a name="connection-attributes"></a>連接屬性
連接屬性是連接的特性。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣地，在超時之前嘗試連接的登入超時時間或等候的秒數，是一個連接屬性。  
  
 連接屬性會設定 **SQLSetConnectAttr** ，並以 **SQLGetConnectAttr**抓取其目前的設定。 如果在載入驅動程式之前呼叫 **SQLSetConnectAttr** ，驅動程式管理員會在其連接結構中儲存屬性，並將它們設定在驅動程式中，做為連接程式的一部分。 應用程式不需要設定任何連接屬性;所有連接屬性都有預設值，其中有些是驅動程式特定的。  
  
 連接屬性可以在連接之前或之後設定，或根據屬性和驅動程式來設定。 登入超時 (SQL_ATTR_LOGIN_TIMEOUT) 適用于連接程式，而且只有在連接之前已設定時才有效。 指定是否要使用 ODBC 資料指標程式庫 (SQL_ATTR_ODBC_CURSORS) 的屬性，以及在連接之前必須設定網路封包大小 (SQL_ATTR_PACKET_SIZE) ，因為 ODBC 資料指標程式庫位於驅動程式管理員和驅動程式之間，因此必須在驅動程式之前載入。  
  
 屬性，可指定資料來源為唯讀或讀寫 (SQL_ATTR_ACCESS_MODE) 而且目前的目錄 (SQL_ATTR_CURRENT_CATALOG) 可以在連接之前或之後設定，這取決於驅動程式。 不過，互通的應用程式會在連接之前設定它們，因為某些驅動程式不支援在連接之後變更這些驅動程式。  
  
 某些連接屬性在建立連接之前會有預設值，其他則沒有。 其中的 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 在連接之後，必須設定轉譯連接屬性 (SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION) 。  
  
 您可以隨時設定所有其他連接屬性。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 函數描述。 呼叫 **SQLSetEnvAttr**時，無法在環境層級上設定 (連接屬性。 ) 
