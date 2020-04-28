---
title: SQL_variant 日期和時間類型的支援 |Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 588fcceb40ea096c549a004c1e2636d0eaf17c6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291663"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>日期和時間類型的 sql_variant 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題描述**SQL_variant**資料類型如何支援增強的日期和時間功能。  
  
 資料行屬性 SQL_CA_SS_VARIANT_TYPE 是用來傳回變數結果資料行的 C 類型。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了一個額外的屬性 SQL_CA_SS_VARIANT_SQL_TYPE，可在實作資料列描述項 (IRD) 中設定變數結果資料行的 SQL 類型。 SQL_CA_SS_VARIANT_SQL_TYPE 也可以在實作參數描述項 (IPD) 中用來指定讓 SQL_C_BINARY C 類型與 SQL_SS_VARIANT 類型繫結之 SQL type of a SQL_SS_TIME2 或 SQL_SS_TIMESTAMPOFFSET 參數的 SQL 類型。  
  
 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 的新類型可以由 SQLColAttribute 設定。 SQLGetDescField 可以傳回 SQL_CA_SS_VARIANT_SQL_TYPE。  
  
 若為結果資料行，驅動程式會從變數轉換成日期/時間類型。 如需詳細資訊，請參閱[從 SQL 轉換為 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。當系結至 SQL_C_BINARY 時，緩衝區長度必須夠大，才能接收對應至 SQL 類型的結構。  
  
 對於 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 參數，驅動程式會將 C 值轉換成**SQL_variant**值，如下表所述。 如果某個參數繫結成 SQL_C_BINARY 而且伺服器類型為 SQL_SS_VARIANT，除非應用程式已經將 SQL_CA_SS_VARIANT_SQL_TYPE 設定為其他 SQL 類型，否則它就會被視為二進位值。 在此情況下，系統會優先使用 SQL_CA_SS_VARIANT_SQL_TYPE。也就是說，如果已設定 SQL_CA_SS_VARIANT_SQL_TYPE，它就會覆寫從 C 類型推算出變數 SQL 類型的預設行為。  
  
|C 類型|伺服器類型|評價|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_STINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SSHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_ULONG|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_SBIGINT|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_DOUBLE|FLOAT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_UTINYINT|TINYINT|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_BINARY|varbinary|不會設定 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> [小數值數] 設定為 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*參數）。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> [小數值數] 設定為 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*參數）。|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|[小數值數] 設定為 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*參數）。|  
|SQL_C_NUMERIC|decimal|Precision 設定為 SQL_DESC_PRECISION （ **SQLBindParameter**的*ColumnSize*參數）。<br /><br /> 將擴展集設定為 SQL_DESC_SCALE （SQLBindParameter 的*DecimalDigits*參數）。|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE 會被忽略|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
