---
title: 環境、 連接和陳述式屬性 |Microsoft 文件
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
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b8e3ee068d160269336de15ce1ddef3e7c78d58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911083"
---
# <a name="environment-connection-and-statement-attributes"></a>環境、 連接和陳述式屬性
ODBC 定義環境、 連線或陳述式相關聯的屬性的數目。  
  
 環境屬性會影響整個環境中的，例如是否啟用連接共用。 環境屬性設定**SQLSetEnvAttr**和擷取與**SQLGetEnvAttr**。  
  
 連接屬性會影響每個連接個別，例如應如何嘗試連接到資料來源必須在逾時之前等待的驅動程式應該很長。設定連接屬性**SQLSetConnectAttr**和擷取與**SQLGetConnectAttr**。 如需有關連接屬性的詳細資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 陳述式屬性例如是否執行陳述式應該是以非同步方式個別影響每個陳述式。 陳述式屬性設定**SQLSetStmtAttr**和擷取與**SQLGetStmtAttr**。 幾個陳述式屬性是唯讀屬性，而且無法設定。 比方說，用來擷取資料指標中目前資料列數目，SQL_ATTR_ROW_NUMBER 陳述式屬性是唯讀。 如需陳述式屬性的詳細資訊，請參閱[陳述式屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了 ODBC 所定義的屬性，驅動程式可以定義自己的連接和陳述式屬性。 驅動程式定義的屬性必須向開啟群組，以確保兩個驅動程式廠商沒有指派相同的整數值不同，專屬的屬性。 如需詳細資訊，請參閱[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 如需完整的屬性清單，請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 ODBC 函數，它們會影響的描述中也說明了大部分的屬性。
