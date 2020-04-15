---
title: 其他表值參數元資料 |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b52f83e36c315ccd86d1516df9e11b913c80ba8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304529"
---
# <a name="additional-table-valued-parameter-metadata"></a>其他資料表值參數中繼資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  若要檢索表值參數的元數據,應用程式將調用 SQL 程式列。 對於表值參數,SQL程式列將返回一行。 添加了兩[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]個附加列(SS_TYPE_CATALOG_NAME和SS_TYPE_SCHEMA_NAME,以便為與表值參數關聯的表類型提供架構和目錄資訊。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式專用資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
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
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint 非 NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|整數|NULL|  
|ORDINAL_POSITION|整數不是 NULL|參數的序數位置。|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的目錄。|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) 非 NULL|包含資料表值參數資料表類型之類型定義的結構描述。|  
  
 WVarchar 資料行在 ODBC 規格中定義為 Varchar，但是實際上在所有最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式中會傳回為 Wvarchar。 當 Unicide 支援加入到 ODBC 3.5 規格，但是尚未明確呼叫時，會進行此變更。  
  
 要取得表值參數的其他元資料,應用程式使用目錄函數 SQLColumns 和 SQLPrimaryKeys。 針對資料表值參數呼叫這些函數之前，應用程式必須將陳述式屬性 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE。 此值表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料。 然後,應用程式將表值參數的TYPE_NAME作為*表名稱*參數傳遞。 SS_TYPE_CATALOG_NAME和SS_TYPE_SCHEMA_NAME分別與*目錄名稱*和*架構名稱*參數一起使用,以標識表值參數的目錄和架構。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 使用包含伺服器元件的目錄對 SQLColumns 或 SQL 主要密鑰的呼叫將失敗。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
