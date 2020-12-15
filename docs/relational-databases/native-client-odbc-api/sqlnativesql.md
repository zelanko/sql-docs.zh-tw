---
description: SQLNativeSql
title: SQLNativeSql |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cebaef8091839467fa818f13516efee384b089c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485080"
---
# <a name="sqlnativesql"></a>SQLNativeSql
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式不需要造訪伺服器，就能滿足 **SQLNativeSql** 的要求。 此函數可有效率地測試 SQL 陳述式的語法。 語法檢查無法判斷 SQL 語句中的識別碼或運算式的結果是否有效，且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQLNativeSql** 傳回的原生 SQL 可能無法執行。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNativeSql 函式](../../odbc/reference/syntax/sqlnativesql-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
