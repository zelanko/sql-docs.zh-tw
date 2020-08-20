---
description: ODBC 服務提供者介面 (SPI) 參考
title: ODBC 服務提供者介面 (SPI) 參考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ef1eea6dd78537169d3394c7d048d1829e8d9a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487351"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服務提供者介面 (SPI) 參考
傳統上，ODBC 定義了應用程式設計介面， (API) 。 API 中的函式可以由應用程式呼叫，且應該在驅動程式管理員和驅動程式內部執行。  
  
 由於加入了驅動程式感知的連接共用功能，ODBC (SPI) 引進了服務提供者介面。 SPI 中的函式是用來進行驅動程式管理員與驅動程式之間的通訊。 SPI 函式是由驅動程式所執行;驅動程式管理員不會將 SPI 函式公開給應用程式。 應用程式不應該直接呼叫這些函式。  
  
 包含用於 ODBC 驅動程式開發的 sqlspi .h。  
  
 本節涵蓋下列主題  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驅動程式管理員連線共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
