---
description: ODBC 服務提供者介面摘要
title: ODBC 服務提供者介面摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00d15d33fba1e697eebbe6a640c4f8a4d8eadea7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487341"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服務提供者介面摘要
下表描述 ODBC 服務提供者介面函數。 如需每個函式之語法和語義的詳細資訊，請參閱 [ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函式名稱|用途|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|與 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同，但它會在連接資訊權杖上設定屬性，而不是在連接控制碼上設定。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|將連接字串設定為應用程式 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 呼叫的連接資訊權杖。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|將資料來源、使用者識別碼和密碼設定為應用程式 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 呼叫的連接資訊權杖。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|捕獲集區識別碼。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|判斷驅動程式是否可以重複使用連接集區中的現有連接。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果集區中沒有可重複使用的連接，請建立新的連線。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知驅動程式集區識別碼已超時。|
