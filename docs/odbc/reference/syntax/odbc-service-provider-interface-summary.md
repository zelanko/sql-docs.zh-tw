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
ms.openlocfilehash: 0a97bed3bb921b9c881a98d8d9a9031ef7630f26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111900"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服務提供者介面摘要
下表描述 ODBC 服務提供者介面函數。 如需有關每個函式之語法和語義的詳細資訊，請參閱[ODBC 服務提供者介面（SPI）參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函式名稱|目的|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|與[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同，但它會在連接資訊 token 上設定屬性，而不是在連接控制碼上。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|將連接字串設定為應用程式[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫的連接資訊 token。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|將資料來源、使用者識別碼和密碼設定為應用程式[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫的連接資訊 token。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|抓取集區識別碼。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|判斷驅動程式是否可以重複使用連接集區中的現有連接。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果無法重複使用集區中的連接，請建立新的連接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知驅動程式已將集區識別碼計時。|
