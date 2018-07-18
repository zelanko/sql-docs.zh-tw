---
title: 連接屬性 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90119e72be2ea64da85fc6790b4e28b9e679a8f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909813"
---
# <a name="connection-attributes"></a>連接屬性
連接屬性是連接的特性。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣地，登入逾時或嘗試連接之前，在逾時等待的秒數是連接屬性。  
  
 設定連接屬性**SQLSetConnectAttr**和其目前的設定擷取**SQLGetConnectAttr**。 如果**SQLSetConnectAttr**之前呼叫驅動程式會載入驅動程式管理員存放其連接結構中的屬性，並設定這些驅動程式中的連線程序的一部分。 沒有需要應用程式設定任何連接屬性;所有連接屬性都有預設值，其中有些是驅動程式專屬。  
  
 連線，或請根據屬性和驅動程式之前或之後，可以設定連接屬性。 登入逾時 (SQL_ATTR_LOGIN_TIMEOUT) 套用至連線程序，並有效才設定連線之前。 指定是否要使用 ODBC 資料指標程式庫 (SQL_ATTR_ODBC_CURSORS) 和網路封包大小 (SQL_ATTR_PACKET_SIZE) 的屬性必須設定連接之前，因為 ODBC 資料指標程式庫位於驅動程式管理員與驅動程式和因此必須在載入之前驅動程式。  
  
 若要指定資料來源是唯讀還是讀寫 (SQL_ATTR_ACCESS_MODE) 和目前的目錄 (SQL_ATTR_CURRENT_CATALOG) 您可以將之前或連接之後，根據驅動程式屬性。 不過，互通的應用程式設定認證後才能連接因為有些驅動程式不支援變更這些連接之後。  
  
 有些連接屬性具有預設值，才能建立連接，有些則不用。 這些是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 連接之後，必須設定轉譯連接屬性 （SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION）。  
  
 所有其他連接屬性可以在任何時間設定。 如需詳細資訊，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函式描述。 (無法由呼叫環境層級上設定的連接屬性**SQLSetEnvAttr**。)
