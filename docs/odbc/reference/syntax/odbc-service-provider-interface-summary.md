---
title: ODBC 服務提供者介面摘要 |微軟文件
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
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298895"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服務提供者介面摘要
下表描述了ODBC服務提供者介面功能。 有關每個函數的語法和語義的詳細資訊,請參閱[ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函式名稱|目的|  
|-------------------|-------------|  
|[SQLSetConnectattrFordbcinfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|與[SQLSetConnect Attr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同,但它在連接資訊權杖上而不是在連接句柄上設置屬性。|  
|[SQLSet 驅動程式連線資訊](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|將連接字串設定到應用程式的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫的連接資訊權杖中。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|將數據源、使用者 ID 和密碼設定到應用程式的[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)調用的連接資訊權杖中。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|檢索池 ID。|  
|[SQLRate 連線](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|確定驅動程式是否可以重用連接池中的現有連接。|  
|[SQLPool 連接](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果池中無法重用連接,則創建新連接。|  
|[SQL 清理連線池 ID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知驅動程式池 ID 已超時。|
