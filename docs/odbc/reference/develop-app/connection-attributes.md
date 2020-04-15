---
title: 連接屬性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299039"
---
# <a name="connection-attributes"></a>連接屬性
連接屬性是連接的特徵。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣,登錄超時,或嘗試連接時等待的秒數,在超時之前,是一個連接屬性。  
  
 連接屬性是使用**SQLSetConnectAttr**設置的,並且其當前設置使用**SQLGetConnectAttr**檢索。 如果在載入驅動程式之前呼叫**SQLSetConnectAttr 驅動**程式管理員將屬性儲存在其連接結構中,並將其設置為驅動程式中的連接過程的一部分。 沒有要求應用程式設置任何連接屬性;所有連接屬性都有預設值,其中一些是特定於驅動程式的。  
  
 連接屬性可以在連接之前或之後設置,也可以設置,具體取決於屬性和驅動程式。 登錄超時(SQL_ATTR_LOGIN_TIMEOUT)適用於連接過程,僅在連接前設置時才有效。 在連接之前,必須設置指定是否使用 ODBC 游標庫 (SQL_ATTR_ODBC_CURSORS) 和網路數據包大小 (SQL_ATTR_PACKET_SIZE)的屬性,因為 ODBC 游標庫位於驅動程式管理器和驅動程式之間,因此必須在驅動程式之前載入。  
  
 指定數據源是唯讀還是讀寫 (SQL_ATTR_ACCESS_MODE) 和當前目錄 (SQL_ATTR_CURRENT_CATALOG) 的屬性可以在連接之前或之後設置,具體取決於驅動程式。 但是,可互通的應用程式在連接前設置它們,因為某些驅動程式不支援在連接後更改它們。  
  
 某些連接屬性在建立連接之前具有預設值,而其他連接屬性則沒有預設值。 那些做是SQL_ATTR_ACCESS_MODE,SQL_ATTR_AUTOCOMMIT,SQL_ATTR_LOGIN_TIMEOUT,SQL_ATTR_ODBC_CURSORS,SQL_ATTR_TRACE和SQL_ATTR_TRACEFILE。  
  
 連接後必須設置轉換連接屬性(SQL_ATTR_TRANSLATE_DLL和SQL_ATTR_TRANSLATE_OPTION)。  
  
 可以隨時設置所有其他連接屬性。 有關詳細資訊,請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函數說明。 (無法透過呼叫**SQLSetEnvAttr**在環境等級設定連接屬性。
