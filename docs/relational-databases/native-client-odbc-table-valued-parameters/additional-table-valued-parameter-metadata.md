---
title: 其他資料表值參數中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a83df9dde4ada571b0fc39f6ac8e45c49d9ac17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73777904"
---
# <a name="additional-table-valued-parameter-metadata"></a>其他資料表值參數中繼資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  為了取得資料表值參數的中繼資料，應用程式會呼叫 SQLProcedureColumns。 若為數據表值參數，SQLProcedureColumns 會傳回單一資料列。 已加入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]兩個額外的特定資料行 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME，以提供與資料表值參數相關聯之資料表類型的架構和目錄資訊。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式專用資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 下表列出對於資料表值參數相當重要的資料行。  
  
|資料行名稱|資料類型|值/註解|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint 非 NULL|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) 非 NULL|資料表值參數的類型名稱。|  
|COLUMN_SIZE|整數|NULL|  
|BUFFER_LENGTH|整數|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|Smallint 非 NULL|SQL_NULLABLE|  
|備註|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint 非 NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|整數|NULL|  
|ORDINAL_POSITION|整數不是 NULL|參數的序數位置。|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的目錄。|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的結構描述。|  
  
 WVarchar 資料行在 ODBC 規格中定義為 Varchar，但是實際上在所有最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式中會傳回為 Wvarchar。 當 Unicide 支援加入到 ODBC 3.5 規格，但是尚未明確呼叫時，會進行此變更。  
  
 若要取得資料表值參數的其他中繼資料，應用程式會使用 SQLColumns 和 SQLPrimaryKeys 目錄函數。 針對資料表值參數呼叫這些函數之前，應用程式必須將陳述式屬性 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE。 此值表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料。 然後，應用程式會傳遞資料表值參數的 TYPE_NAME 做為*TableName*參數。 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 分別與*CatalogName*和*SchemaName*參數搭配使用，以識別資料表值參數的目錄和架構。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 使用包含伺服器元件的目錄呼叫 SQLColumns 或 SQLPrimaryKeys 將會失敗。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
