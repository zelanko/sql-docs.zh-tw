---
title: 環境、 連接和陳述式屬性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77be71458eb10e97a82c925d34141a7bcaf1dc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943001"
---
# <a name="environment-connection-and-statement-attributes"></a>環境、連線和陳述式屬性
ODBC 定義多個環境、 連線或陳述式相關聯的屬性。  
  
 環境屬性會影響整個環境中的，例如是否啟用連接共用。 設定環境屬性**SQLSetEnvAttr**和與擷取**SQLGetEnvAttr**。  
  
 連接屬性會影響每個連接個別，例如，如何將驅動程式應該嘗試連接到資料來源，逾時之前等待的時間。設定連接屬性**SQLSetConnectAttr**和與擷取**SQLGetConnectAttr**。 如需有關連接屬性的詳細資訊，請參閱 <<c0> [ 連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 陳述式屬性例如是否陳述式應該是以非同步方式執行，請以個別影響每個陳述式。 陳述式屬性設定**SQLSetStmtAttr**和與擷取**SQLGetStmtAttr**。 幾個陳述式屬性是唯讀屬性，且無法設定。 比方說，SQL_ATTR_ROW_NUMBER 陳述式屬性，來擷取的資料指標中目前資料列數目，會是唯讀。 如需詳細的陳述式屬性的詳細資訊，請參閱[陳述式屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了 ODBC 所定義的屬性，驅動程式可以定義自己的連接和陳述式屬性。 驅動程式定義的屬性必須向開啟群組，以確保兩個驅動程式供應商不會在不同的專屬屬性指派相同的整數值。 如需詳細資訊，請參閱 <<c0> [ 驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 如需的屬性完整清單，請參閱 < [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，並[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 它們會影響的 ODBC 函式的描述中也說明大部分的屬性。
