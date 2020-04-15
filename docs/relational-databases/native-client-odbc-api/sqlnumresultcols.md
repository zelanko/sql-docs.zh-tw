---
title: SQLNumResultCols |微軟文件
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
ms.openlocfilehash: 2b56dad6564bad751829497117cc74553806b244
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302379"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於已執行的語句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],本機用戶端 ODBC 驅動程式不會訪問伺服器來報告結果集中的列數。 在這種情況下 **,SQLNumResultCols**不會導致伺服器往返。 與[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)和[SQLColAttribute 一](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)樣,在已準備好但未執行語句時調用**SQLNumResultCols**會生成伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 應為每個集調用**SQLNumResultCols。** 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 有關處理多個結果集傳回的詳細資訊,請參閱[SQLMore 結果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 資料庫引擎的改進從 SQLNumResultCols[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始 ,可以更精確地描述預期結果。 這些更準確的結果可能與 SQLNumResultCols 在 以前的版本中傳[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]回的值不同 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNumResultCols 函數](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
