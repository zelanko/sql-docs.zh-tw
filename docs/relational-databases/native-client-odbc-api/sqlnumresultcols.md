---
description: SQLNumResultCols
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a489dda3eab0028ab6c3d0d4fb16b82a10481d1
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810924"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  對於執行的語句而言， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式不會造訪伺服器來報告結果集中的資料行數目。 在此情況下， **SQLNumResultCols** 不會造成伺服器往返。 如同 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 和 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)，在備妥但未執行的語句上呼叫 **SQLNumResultCols** 會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 應針對每個集合呼叫**SQLNumResultCols** 。 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需處理多個結果集傳回的詳細資訊，請參閱 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 資料庫引擎的增強功能從 [ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 允許 SQLNumResultCols] 取得預期結果更精確的描述。 這些更精確的結果可能與舊版的 SQLNumResultCols 所傳回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNumResultCols 函式](../../odbc/reference/syntax/sqlnumresultcols-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
