---
title: "其他資料表值參數中繼資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffec7d671d4005b2af89b3d1767992eaf36ad11b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="additional-table-valued-parameter-metadata"></a>其他資料表值參數中繼資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  若要擷取資料表值參數的中繼資料，應用程式會呼叫 SQLProcedureColumns。 資料表值參數，SQLProcedureColumns 傳回的單一資料列。 兩個額外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-已加入專用資料行： SS_TYPE_CATALOG_NAME 與 ss_type_schema_name，藉以提供與資料表值參數相關聯的資料表類型之結構描述與目錄資訊。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式專用資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 下表列出對於資料表值參數相當重要的資料行。  
  
|資料行名稱|資料類型|值/註解|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint 非 NULL|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) 非 NULL|資料表值參數的類型名稱。|  
|COLUMN_SIZE|Integer|NULL|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|Smallint 非 NULL|SQL_NULLABLE|  
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint 非 NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|Integer|NULL|  
|ORDINAL_POSITION|整數不是 NULL|參數的序數位置。|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的目錄。|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的結構描述。|  
  
 WVarchar 資料行在 ODBC 規格中定義為 Varchar，但是實際上在所有最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式中會傳回為 Wvarchar。 當 Unicide 支援加入到 ODBC 3.5 規格，但是尚未明確呼叫時，會進行此變更。  
  
 若要取得資料表值參數的其他中繼資料，應用程式會使用目錄函數 SQLColumns 和 SQLPrimaryKeys。 針對資料表值參數呼叫這些函數之前，應用程式必須將陳述式屬性 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE。 此值表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料。 應用程式接著會傳遞做為資料表值參數的 TYPE_NAME *TableName*參數。 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會搭配*CatalogName*和*SchemaName*參數，分別以指定的目錄和資料表值參數的結構描述。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 呼叫 SQLColumns 或 SQLPrimaryKeys 與包含的伺服器元件的目錄將會失敗。  
  
## <a name="see-also"></a>請參閱  
 [資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
