---
title: 環境、連接和語句屬性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300928"
---
# <a name="environment-connection-and-statement-attributes"></a>環境、連線和陳述式屬性
ODBC 定義了許多與環境、連接或語句關聯的屬性。  
  
 環境屬性會影響整個環境,例如是否啟用了連接池。 環境屬性使用**SQLSetEnvAttr**設置,並使用**SQLGetEnvAttr**檢索。  
  
 連接屬性會單獨影響每個連接,例如驅動程式在嘗試連接到數據源時應等待多長時間,然後再超時。連接屬性使用**SQLSetConnect Attr**設置,並使用**SQLGetConnectAttr**檢索。 有關連線屬性的詳細資訊,請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 語句屬性單獨影響每個語句,例如是否應非同步執行語句。 語句屬性使用**SQLSetStmtAttr**設置,並使用**SQLGetStmtAttr**檢索。 少數語句屬性是唯讀屬性,無法設置。 例如,用於檢索游標中當前行數SQL_ATTR_ROW_NUMBER語句屬性是唯讀的。 關於敘述屬性的詳細資訊,請參考[敘述屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了由 ODBC 定義的屬性外,驅動程式還可以定義其自己的連接和語句屬性。 驅動程式定義的屬性必須註冊到 Open Group,以確保兩個驅動程式供應商不會將相同的整數值分配給不同的專有屬性。 有關詳細資訊,請參閱[特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有關屬性的完整清單,請參閱[SQLSetEnvAttr、SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)和[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 大多數屬性在它們影響的 ODBC 函數的描述中也作了描述。
