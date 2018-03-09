---
title: "配置環境控制代碼 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: "29"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 853600caebf537d1d7c63165ce2f7caf2ac49fbd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="allocating-an-environment-handle"></a>配置環境控制代碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  應用程式必須先初始化 ODBC 環境並配置環境控制代碼，然後才能呼叫任何 ODBC 函數。 在 ODBC 中，這是其他控制代碼的全域內容控制代碼和預留位置。 您可以呼叫**SQLAllocHandle**與*HandleType*參數設定為 SQL_HANDLE_ENV 並*InputHandle*設定為 SQL_NULL_HANDLE。  
  
 配置環境控制代碼之後，應用程式必須設定環境屬性來指出它將使用的 ODBC 函數呼叫版本。 若要使用 ODBC 3。*x*函式，呼叫[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)與*屬性*參數設定為 SQL_ATTR_ODBC_VERSION 並*ValuePtr*設 SQL_OV_ODBC3。  
  
## <a name="see-also"></a>另請參閱  
 [通訊使用 SQL Server &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
