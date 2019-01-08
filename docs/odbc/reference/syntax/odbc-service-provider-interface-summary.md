---
title: ODBC 服務提供者介面摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5f3c133b105c905b79589d86952658b6d39f0f6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52390441"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服務提供者介面摘要
下表描述 ODBC 服務提供者介面函式。 如需語法和語意，每個函式的詳細資訊，請參閱[ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函數名稱|用途|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|與相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，但它的連線資訊語彙基元而不是在連接控制代碼上設定的屬性。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|設定的連接字串至應用程式的連線資訊語彙基元[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|設定資料來源、 使用者識別碼和密碼到應用程式的連線資訊語彙基元[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|擷取集區識別碼。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|判斷驅動程式可以重複使用現有的連接，連接集區中。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果集區中的沒有連線可以重複使用，請建立新的連接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知逾時的集區識別碼的驅動程式。|
