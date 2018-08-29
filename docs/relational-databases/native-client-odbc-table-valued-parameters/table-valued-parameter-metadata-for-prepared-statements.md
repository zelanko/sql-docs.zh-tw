---
title: 針對已備妥的陳述式資料表值參數中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54617a7649ad055002c5b84522ce231dbf6bd879
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110700"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>已備妥之陳述式的資料表值參數中繼資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  應用程式可以取得已備妥之程序呼叫透過 SQLNumParams 和 SQLDescribeParam 的中繼資料。 資料表值參數，如*DataTypePtr*設定為 SQL_SS_TABLE。 其他中繼資料可透過 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 的 SQLGetDescField。  
  
 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可以搭配 SQLColumns 來取得與資料表值參數相關聯的資料表類型的資料行中繼資料。 在此情況下，SQL_SOPT_SS_NAME_SCOPE 必須設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE SQLColumns 呼叫之前。 當應用程式完成資料表值參數資料行中繼資料的擷取時，SQL_SOPT_SS_NAME_SCOPE 應該設回預設值 SQL_SS_NAME_SCOPE_TABLE。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 也可以搭配 CLR 使用者定義型別參數使用。  
  
 您無法針對不是預存程序呼叫的已備妥陳述式來取得資料表值參數中繼資料。 如果您嘗試這樣做，應用程式會傳回 SQL_ERROR，其中包含 SQLSTATE 42000 和「語法錯誤或違規存取」訊息。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
