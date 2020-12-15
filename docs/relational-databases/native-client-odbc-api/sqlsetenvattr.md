---
description: SQLSetEnvAttr
title: SQLSetEnvAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba2b49fa3e5fbc8be5ed21a42604993ce0be6755
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438691"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Odbc 程式設計 [人員參考](../../odbc/reference/odbc-programmer-s-reference.md) 定義 odbc 驅動程式如何從寫入 odbc 2 的應用程式中，解讀 **SQLSetEnvAttr** 屬性規格。*x* 或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式符合這些規則。  
  
 **SQLSetEnvAttr** 所控制的其中一個屬性是是否要使用連接共用。 如果連接共用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式搭配使用，則在使用 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或 **SQLConnect** 連接時， *DriverCompletion* 參數必須設定為 SQL_DRIVER_NOPROMPT。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetEnvAttr 函式](../../odbc/reference/syntax/sqlsetenvattr-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
