---
description: 資料指標並行 (ODBC)
title: 資料指標並行 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 324e193ff8ac1f98c00f8569c0da2a3c93f56ad0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420662"
---
# <a name="cursor-concurrency-odbc"></a>資料指標並行 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  資料指標作業跟資料指標類型一樣，會受到應用程式設定之並行選項的影響。 並行選項是使用 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)的 SQL_ATTR_CONCURRENCY 選項設定。 並行類型為：  
  
-   唯讀 (SQL_CONCUR_READONLY)  
  
-   值 (SQL_CONCUR_VALUES)  
  
-   資料列版本 (SQL_CONCUR_ROWVER)  
  
-   鎖定 (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
