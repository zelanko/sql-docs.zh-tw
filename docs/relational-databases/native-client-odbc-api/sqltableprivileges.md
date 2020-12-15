---
description: SQLTablePrivileges
title: SQLTablePrivileges |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f7fd6b49d4e7118fb429071df23633c2c2ac0c7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465069"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLTablePrivileges** 可以在靜態資料指標上執行。 嘗試在可更新的 (索引鍵集驅動或動態) 上執行 **SQLTablePrivileges** 時，會傳回 SQL_SUCCESS_WITH_INFO 表示資料指標類型已經變更。  
  
 > Native Client ODBC 驅動程式會藉由接受 *CatalogName* 參數的兩部分名稱，來支援連結伺服器上資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQLTablePrivileges 函式] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API 實作詳細資料](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
