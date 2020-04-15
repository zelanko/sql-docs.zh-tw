---
title: 游標事務隔離等級 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49ad51f271e80017420db978f9cac2d867712d8c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302861"
---
# <a name="cursor-transaction-isolation-level"></a>資料指標交易隔離等級
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  資料指標的完整鎖定行為是以並行屬性之間的互動以及用戶端所設定的交易隔離等級為基礎。 ODBC 用戶端使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION或SQL_COPT_SS_TXN_ISOLATION屬性設定事務隔離等級。 特定資料指標環境的鎖定行為藉由結合以下各項來決定：並行的鎖定行為，以及交易隔離層級選項。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機客戶端 ODBC 驅動程式支援以下游標交易隔離等級:  
  
-   讀取認可 (SQL_TXN_READ_COMMITTED)  
  
-   讀取未認可 (SQL_TXN_READ_UNCOMMITTED)  
  
-   可重覆讀取 (SQL_TXN_REPEATABLE_READ)  
  
-   可序列化 (SQL_TXN_SERIALIZABLE)  
  
-   快照集 (SQL_TXN_SS_SNAPSHOT)  
  
 請注意,ODBC API 指定其他事務隔離級別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)],但[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機 用戶端ODBC驅動程式不支援這些級別。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
