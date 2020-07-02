---
title: SQLEndTran |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a668d69434d78dab1a1494a785023e84736e32af
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789311"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當**SQLEndTran**認可或回復作業時，Native Client ODBC 驅動程式會關閉語句的相關資料指標。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業時，語句相關資料指標的行為是由驅動程式特定的 ODBC 連接屬性值所決定，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設定。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 的執行詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函數](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
