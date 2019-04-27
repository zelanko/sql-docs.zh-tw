---
title: ODBC 服務提供者介面 (SPI) 參考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e3d83f0aa27641c9dde164f51319a0e78d456ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653246"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服務提供者介面 (SPI) 參考
傳統上，ODBC 會定義應用程式開發介面 (API)。 應用程式可以呼叫 API 中的函式，它們應該實作在驅動程式管理員和驅動程式。  
  
 可感知驅動程式的連接集區的功能加入，ODBC 導入了服務提供者介面 (SPI)。 在 SPI 的函式用於驅動程式管理員和驅動程式之間的通訊。 SPI 函式會藉由將驅動程式;驅動程式管理員不會公開 SPI 函式應用程式。 應用程式不應該直接呼叫這些函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
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
 [開發 ODBC 驅動程式中的連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驅動程式管理員連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
