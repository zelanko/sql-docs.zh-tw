---
title: "ODBC 服務提供者介面摘要 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82610a48532970f14800574155db89929e371baf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服務提供者介面摘要
下表描述 ODBC 服務提供者介面函式。 如需語法和語意，每個函式的詳細資訊，請參閱[ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函數名稱|目的|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|與相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，但是它上的連線資訊語彙基元而非連接控制代碼上設定的屬性。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|設定連線資訊語彙基元中的應用程式的連接字串[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|設定資料來源、 使用者識別碼和密碼的應用程式的連線資訊語彙基元[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|擷取集區識別碼。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|判斷驅動程式可以重複使用現有的連接，連接集區中。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果沒有連接集區中的可以重複使用，請建立新的連接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|告知記憶體集區識別碼逾時的驅動程式。|
