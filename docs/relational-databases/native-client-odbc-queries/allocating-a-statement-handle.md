---
description: 配置陳述式控制代碼
title: 配置語句控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8e48700a57f6ec9a3c577f653490cdfc9319381
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499163"
---
# <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在應用程式可以執行陳述式之前，它必須配置陳述式控制代碼。 它會藉由呼叫 **SQLAllocHandle** ，並將 *HandleType* 參數設定為 SQL_HANDLE_STMT，並將 *InputHandle* 指向連接控制碼來執行此工作。  
  
 陳述式屬性是陳述式控制代碼的特性。 範例陳述式屬性可以包含使用書籤和搭配陳述式結果集使用的資料指標種類。 語句屬性是使用 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設定的，而且其目前的設定是使用 [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)抓取。 應用程式不需要設定任何陳述式屬性；所有陳述式屬性都有預設值，而且有些是驅動程式專屬的。  
  
 使用數個 ODBC 陳述式與連接選項時請小心。 將*fOption*設定為 SQL_ATTR_LOGIN_TIMEOUT 會呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) ，以控制應用程式在等待建立連接時等候連接逾時的時間， (0 指定無限等待) 。 回應時間緩慢的網站可以將這個值設高一點，以確認連接有充足的時間可以完成。 不過，如果驅動程式無法連接，間隔應該一律夠低，才能在合理的時間內回應使用者。  
  
 將*fOption*設定為 SQL_ATTR_QUERY_TIMEOUT 的呼叫**SQLSetStmtAttr**會設定查詢逾時間隔，以協助保護伺服器和使用者免于長時間執行的查詢。  
  
 呼叫 **SQLSetStmtAttr** 時， *fOption* 設定為 SQL_ATTR_MAX_LENGTH 會限制個別語句可以取出的 **文字** 和 **影像** 資料量。 將*fOption*設定為 SQL_ATTR_MAX_ROWS 的呼叫**SQLSetStmtAttr**也會將資料列集限制為前*n*個數據列（如果這是應用程式所需的資料列）。 請注意，設定 SQL_ATTR_MAX_ROWS 會使驅動程式對伺服器發出 SET ROWCOUNT 陳述式。 這會影響所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語句，包括觸發程式和更新。  
  
 當您要設定這些選項時，請小心使用。 連接控制代碼上的所有陳述式控制代碼對於 SQL_ATTR_MAX_LENGTH 和 SQL_ATTR_MAX_ROWS 最好都有相同的設定。 如果驅動程式從陳述式控制代碼切換到包含這些選項不同值的其他控制代碼，驅動程式必須產生適當的 SET TEXTSIZE 和 SET ROWCOUNT 陳述式才能變更設定。 驅動程式無法將這些陳述式放在與使用者 SQL 陳述式相同的批次中，因為使用者 SQL 陳述式可能包含必須是批次中第一個陳述式的陳述式。 驅動程式必須以單獨的批次傳送 SET TEXTSIZE 和 SET ROWCOUNT 陳述式，這樣會對伺服器自動產生額外的往返。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行查詢 ](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
