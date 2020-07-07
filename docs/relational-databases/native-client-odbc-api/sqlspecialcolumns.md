---
title: SQLSpecialColumns |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24661c0937c0af83d39831b60b535bd58ebcc626
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012386"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當要求資料列識別碼（*IdentifierType* SQL_BEST_ROWID）時， **SQLSpecialColumns**會針對除了 SQL_SCOPE_CURROW 以外的任何要求範圍，傳回空的結果集（無資料列）。 產生的結果集表示資料行只有在這個範圍中才是有效的。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援識別碼的虛擬資料行。 **SQLSpecialColumns**結果集會將所有資料行識別為 SQL_PC_NOT_PSEUDO。  
  
 **SQLSpecialColumns**可以在靜態資料指標上執行。 嘗試在可更新的（索引鍵集驅動或動態）上執行**SQLSpecialColumns**時，會傳回 SQL_SUCCESS_WITH_INFO 表示資料指標類型已變更。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSpecialColumns 支援  
 如需日期/時間類型 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH 和 DECIMAL_DIGTS 之資料行傳回值的相關資訊，請參閱[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需更多一般資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSpecialColumns 支援  
 **SQLSpecialColumns**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSpecialColumns 函式](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
