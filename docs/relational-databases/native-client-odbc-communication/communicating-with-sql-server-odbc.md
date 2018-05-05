---
title: 與 SQL Server (ODBC) 通訊 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3cf1b57043fe9333d1b0da73a65aae1e251f00fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="communicating-with-sql-server-odbc"></a>與 SQL Server 進行通訊 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 應用程式的執行個體進行通訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必須配置環境和處理，並且連接到資料來源連接。 建立連接之後，應用程式可以將查詢傳送到伺服器，並處理任何結果集。 當應用程式使用資料來源完畢時，它會中斷與資料來源的連接，並釋出連接控制代碼。 當應用程式釋出其所有連接控制代碼時，它會釋出環境控制代碼。  
  
 應用程式可以連接到任何數目的資料來源。 應用程式可以使用驅動程式與資料來源的組合、相同的驅動程式與資料來源組合，甚至相同驅動程式與相同資料來源的多個連接。  
  
 您可以下載[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 範例從[SQL Server 下載](http://go.microsoft.com/fwlink/?LinkId=62796)MSDN 上的頁面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [配置環境控制代碼](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [配置連接控制代碼](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 資料來源](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [連接到資料來源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [從資料來源中斷連接](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
