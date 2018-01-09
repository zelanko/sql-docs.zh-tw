---
title: "SQLNumResultCols |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b4cfc7416b2e4438cc8462353e5f9bea6e125a7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  對於執行的陳述式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不會造訪伺服器來報告結果集中的資料行數目。 在此情況下， **SQLNumResultCols**不會造成伺服器往返。 像[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)和[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)，則呼叫**SQLNumResultCols**上備妥但未執行的陳述式會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 **SQLNumResultCols**應該針對每個集呼叫。 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需有關處理多個結果集傳回，請參閱[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 開始 database engine 中的增強功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 SQLNumResultCols 以取得更精確的預期結果的描述。 這些更精確的結果，在舊版的 SQLNumResultCols 傳回的值可能會有所不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>請參閱  
 [SQLNumResultCols 函數](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
