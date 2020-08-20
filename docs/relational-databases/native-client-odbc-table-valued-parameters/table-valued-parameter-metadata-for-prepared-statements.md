---
description: 已備妥之陳述式的資料表值參數中繼資料
title: TVP 備妥之語句的中繼資料
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c93614fa84a1758586deb72382dde042d40dd827
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455859"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>已備妥之陳述式的資料表值參數中繼資料
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  應用程式可以透過 SQLNumParams 和 SQLDescribeParam 取得備妥程序呼叫的中繼資料。 若為數據表值參數， *DataTypePtr* 會設定為 SQL_SS_TABLE。 您可以透過 SQLGetDescField 取得額外的中繼資料，以取得 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可以與 SQLColumns 搭配使用，以取得與資料表值參數相關聯之資料表類型的資料行中繼資料。 在此情況下，必須在呼叫 SQLColumns 之前將 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE。 當應用程式完成資料表值參數資料行中繼資料的擷取時，SQL_SOPT_SS_NAME_SCOPE 應該設回預設值 SQL_SS_NAME_SCOPE_TABLE。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 也可以搭配 CLR 使用者定義型別參數使用。  
  
 您無法針對不是預存程序呼叫的已備妥陳述式來取得資料表值參數中繼資料。 如果您嘗試這樣做，應用程式會傳回 SQL_ERROR，其中包含 SQLSTATE 42000 和「語法錯誤或違規存取」訊息。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
