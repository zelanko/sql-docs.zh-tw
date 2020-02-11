---
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5ec47c112a41d579710a42c1913785d794f040c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73786035"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於執行的語句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式不會造訪伺服器來報告結果集中的資料行數目。 在此情況下， **SQLNumResultCols**不會造成伺服器往返。 如同[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)和[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)，在已備妥但未執行的語句上呼叫**SQLNumResultCols**會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 應針對每個集合呼叫**SQLNumResultCols** 。 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需有關處理多個結果集傳回的詳細資訊，請參閱[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 從開始，database engine 的改進[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]可讓 SQLNumResultCols 取得預期結果的更精確描述。 這些更精確的結果可能與舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLNumResultCols 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNumResultCols 函式](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
