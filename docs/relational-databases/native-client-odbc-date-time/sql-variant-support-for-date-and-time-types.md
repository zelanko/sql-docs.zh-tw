---
title: 日期和時間類型的 sql_variant 支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 718fc8b9a323ca6b1575021d748afde527dfb872
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062436"
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>日期和時間類型的 sql_variant 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題描述如何**sql_variant**資料型別支援增強型的日期和時間功能。  
  
 資料行屬性 SQL_CA_SS_VARIANT_TYPE 是用來傳回變數結果資料行的 C 類型。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了一個額外的屬性 SQL_CA_SS_VARIANT_SQL_TYPE，可在實作資料列描述項 (IRD) 中設定變數結果資料行的 SQL 類型。 SQL_CA_SS_VARIANT_SQL_TYPE 也可用在實作參數描述項 (IPD) 中指定的 SQL 型別 a SQL_SS_TIME2 或 SQL_SS_TIMESTAMPOFFSET 參數 SQL_C_BINARY C 類型的繫結與 SQL_SS_VARIANT 類型。  
  
 SQLColAttribute 可以設定 SQL_SS_TIME2 和 sql_ss_timestampoffset 這些新的類型。 SQLGetDescField 可以傳回 SQL_CA_SS_VARIANT_SQL_TYPE。  
  
 若為結果資料行，驅動程式會從變數轉換成日期/時間類型。 如需詳細資訊，請參閱 <<c0> [ 從 SQL 轉換成 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。當繫結至 SQL_C_BINARY 時，緩衝區長度必須夠大，無法接收對應至 SQL 類型的結構。  
  
 驅動程式會將 C 值來轉換 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 參數**sql_variant**值，如下表所述。 如果某個參數繫結成 SQL_C_BINARY 而且伺服器類型為 SQL_SS_VARIANT，除非應用程式已經將 SQL_CA_SS_VARIANT_SQL_TYPE 設定為其他 SQL 類型，否則它就會被視為二進位值。 在此情況下，系統會優先使用 SQL_CA_SS_VARIANT_SQL_TYPE。也就是說，如果已設定 SQL_CA_SS_VARIANT_SQL_TYPE，它就會覆寫從 C 類型推算出變數 SQL 類型的預設行為。  
  
|C 類型|伺服器類型|註解|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_STINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SSHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_USHORT|ssNoversion|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_LONG|ssNoversion|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SLONG|ssNoversion|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_ULONG|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SBIGINT|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_FLOAT|REAL|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_DOUBLE|FLOAT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_UTINYINT|TINYINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_BINARY|varbinary|不會設定 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> 小數位數設定為 SQL_DESC_PRECISION ( *DecimalDigits*的參數**SQLBindParameter**)。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> 小數位數設定為 SQL_DESC_PRECISION ( *DecimalDigits*的參數**SQLBindParameter**)。|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|小數位數設定為 SQL_DESC_PRECISION ( *DecimalDigits*的參數**SQLBindParameter**)。|  
|SQL_C_NUMERIC|decimal|有效位數設定為 SQL_DESC_PRECISION ( *ColumnSize*的參數**SQLBindParameter**)。<br /><br /> 小數位數設定為 SQL_DESC_SCALE ( *DecimalDigits* SQLBindParameter 參數)。|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
