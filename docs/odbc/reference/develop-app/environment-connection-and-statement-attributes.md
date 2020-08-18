---
description: 環境、連線和陳述式屬性
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
ms.openlocfilehash: 6bc37e05f2c8847ff9a4828a5d2e9e7456732a41
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482951"
---
# <a name="environment-connection-and-statement-attributes"></a>環境、連線和陳述式屬性
ODBC 會定義許多與環境、連接或語句相關聯的屬性。  
  
 環境屬性會影響整個環境，例如是否啟用連接共用。 環境屬性會以 **SQLSetEnvAttr** 設定，並使用 **SQLGetEnvAttr**抓取。  
  
 連接屬性會個別影響每個連接，例如，在超時之前，驅動程式在嘗試連接到資料來源時應該等待的時間長度。連接屬性會以 **SQLSetConnectAttr** 設定，並使用 **SQLGetConnectAttr**抓取。 如需連接屬性的詳細資訊，請參閱 [連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 語句屬性會個別影響每個語句，例如是否應該以非同步方式執行語句。 語句屬性是使用 **SQLSetStmtAttr** 所設定，並使用 **SQLGetStmtAttr**進行取出。 有幾個語句屬性是唯讀屬性，而且無法設定。 例如，SQL_ATTR_ROW_NUMBER 語句屬性（用於取出資料指標中目前資料列的數目）是唯讀的。 如需語句屬性的詳細資訊，請參閱 [語句屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了 ODBC 所定義的屬性之外，驅動程式還可以定義自己的連接和語句屬性。 驅動程式定義的屬性必須向開放式群組註冊，以確保兩個驅動程式廠商不會將相同的整數值指派給不同的專屬屬性。 如需詳細資訊，請參閱 [驅動程式特定的資料類型、描述項類型、資訊類型、診斷類型與屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 如需屬性的完整清單，請參閱 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 大部分的屬性也會在其所影響之 ODBC 函數的描述中描述。
