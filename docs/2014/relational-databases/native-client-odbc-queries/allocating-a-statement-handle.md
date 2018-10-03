---
title: 配置陳述式控制代碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68e3d7a53f96216d158ddbdb1d1d0ca59db5f81f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215028"
---
# <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼
  在應用程式可以執行陳述式之前，它必須配置陳述式控制代碼。 其做法是呼叫**SQLAllocHandle**具有*HandleType*參數設定為 SQL_HANDLE_STMT 並*InputHandle*指向連接控制代碼。  
  
 陳述式屬性是陳述式控制代碼的特性。 範例陳述式屬性可以包含使用書籤和搭配陳述式結果集使用的資料指標種類。 陳述式屬性設定[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)，以及其目前的設定藉由使用擷取[SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md)。 應用程式不需要設定任何陳述式屬性；所有陳述式屬性都有預設值，而且有些是驅動程式專屬的。  
  
 使用數個 ODBC 陳述式與連接選項時請小心。 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)具有*fOption*將應用程式在等待建立連線 (0 時，等候連接嘗試逾時設定為 SQL_ATTR_LOGIN_TIMEOUT 控制項指定無限期等候）。 回應時間緩慢的網站可以將這個值設高一點，以確認連接有充足的時間可以完成。 不過，如果驅動程式無法連接，間隔應該一律夠低，才能在合理的時間內回應使用者。  
  
 呼叫**SQLSetStmtAttr**具有*fOption*設定為 sql_attr_query_timeout 時設定查詢逾時間隔，以協助防止長時間執行的查詢中的伺服器和使用者。  
  
 呼叫**SQLSetStmtAttr**具有*fOption*設定為 SQL_ATTR_MAX_LENGTH 限制的量**文字**並**映像**資料，可以擷取個別的陳述式。 呼叫**SQLSetStmtAttr**具有*fOption*設定為 SQL_ATTR_MAX_ROWS 也會限制資料列集的第一個*n*資料列，如果這是所有應用程式需要。 請注意，設定 SQL_ATTR_MAX_ROWS 會使驅動程式對伺服器發出 SET ROWCOUNT 陳述式。 這會影響所有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式，包括觸發程序和更新。  
  
 當您要設定這些選項時，請小心使用。 連接控制代碼上的所有陳述式控制代碼對於 SQL_ATTR_MAX_LENGTH 和 SQL_ATTR_MAX_ROWS 最好都有相同的設定。 如果驅動程式從陳述式控制代碼切換到包含這些選項不同值的其他控制代碼，驅動程式必須產生適當的 SET TEXTSIZE 和 SET ROWCOUNT 陳述式才能變更設定。 驅動程式無法將這些陳述式放在與使用者 SQL 陳述式相同的批次中，因為使用者 SQL 陳述式可能包含必須是批次中第一個陳述式的陳述式。 驅動程式必須以單獨的批次傳送 SET TEXTSIZE 和 SET ROWCOUNT 陳述式，這樣會對伺服器自動產生額外的往返。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
