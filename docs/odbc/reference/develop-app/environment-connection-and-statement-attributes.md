---
title: 環境、連接和語句屬性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86cecaf0b82c7b6d15b3f37262507d2cff0c3c10
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300928"
---
# <a name="environment-connection-and-statement-attributes"></a>環境、連線和陳述式屬性
ODBC 會定義一些與環境、連接或語句相關聯的屬性。  
  
 環境屬性會影響整個環境，例如是否啟用連接共用。 環境屬性是以**SQLSetEnvAttr**設定，並使用**SQLGetEnvAttr**來抓取。  
  
 連接屬性會分別影響每個連接，例如，在超時之前，驅動程式在嘗試連接到資料來源時，應該等待的時間長度。連接屬性是以**SQLSetConnectAttr**設定，並使用**SQLGetConnectAttr**來抓取。 如需連接屬性的詳細資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 語句屬性會個別影響每個語句，例如是否應該以非同步方式執行語句。 語句屬性是以**SQLSetStmtAttr**設定，並使用**SQLGetStmtAttr**來抓取。 有些語句屬性是唯讀屬性，無法設定。 例如，SQL_ATTR_ROW_NUMBER 語句屬性（用來取出資料指標中的目前資料列數目）是唯讀的。 如需語句屬性的詳細資訊，請參閱[語句屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了 ODBC 所定義的屬性之外，驅動程式也可以定義自己的連接和語句屬性。 驅動程式定義的屬性必須向開啟的群組註冊，以確保兩個驅動程式廠商不會將相同的整數值指派給不同的專屬屬性。 如需詳細資訊，請參閱[驅動程式特有的資料類型、描述項類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 如需屬性的完整清單，請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 大部分的屬性也會在其影響的 ODBC 函數描述中加以描述。
