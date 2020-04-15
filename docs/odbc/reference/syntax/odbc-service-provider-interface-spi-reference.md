---
title: ODBC 服務提供者介面 (SPI) 參考 |微軟文件
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
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298906"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服務提供者介面 (SPI) 參考
傳統上,ODBC 定義了應用程式程式設計介面 (API)。 API 中的函數可以由應用程式呼叫,它們應在驅動程式管理器和驅動程式內實現。  
  
 隨著驅動程式感知連接池功能的加入,ODBC 引入了服務提供者介面 (SPI)。 SPI 中的函數用於驅動程式管理器和驅動程式之間的通信。 SPI 功能由驅動程序實現;驅動程式管理員不向應用程式公開 SPI 功能。 應用程式不應直接調用這些函數。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
 本節涵蓋下列主題  
  
-   [SQL 清理連線池 ID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPool 連接](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRate 連線](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectattrFordbcinfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSet 驅動程式連線資訊](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [在 ODBC 驅動程式開發連線感池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驅動程式管理員連線共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
