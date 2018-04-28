---
title: JDBC 驅動程式搭配使用陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a70518f53772a37ca9ad2354876a1ec57bea255
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-statements-with-the-jdbc-driver"></a>搭配 JDBC Driver 使用陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可以用來處理資料中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫中有許多種。 利用輸入和輸出參數，JDBC 驅動程式可用來針對資料庫執行 SQL 陳述式，或用於資料庫中呼叫預存程序。 JDBC 驅動程式也支援使用 SQL 逸出序列、更新計數、自動產生的金鑰，以及在批次作業內執行更新。  
  
 JDBC 驅動程式提供三個類別，用於擷取資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫：  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -用於執行不含參數的 SQL 陳述式。  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -（繼承自 SQLServerStatement），用於執行已編譯 SQL 陳述式可能包含 IN 參數。  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -（繼承自 SQLServerPreparedStatement），用來執行預存程序，其中可能包含 IN 參數、 OUT 參數或兩者。  
  
 本節中的主題將討論如何使用每個陳述式三個類別使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)|描述如何使用 JDBC 驅動程式的 SQL 陳述式，使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。|  
|[搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)|描述如何使用 JDBC 驅動程式的預存程序使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。|  
|[使用多個結果集](../../connect/jdbc/using-multiple-result-sets.md)|描述如何使用 JDBC 驅動程式來擷取多個結果集的資料。|  
|[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)|描述如何使用 SQL 逸出序列，例如日期和時間常值及函數。|  
|[使用自動產生的金鑰](../../connect/jdbc/using-auto-generated-keys.md)|描述如何使用自動產生的金鑰。|  
|[執行批次作業](../../connect/jdbc/performing-batch-operations.md)|描述如何使用 JDBC 驅動程式來執行批次作業。|  
|[處理複雜陳述式](../../connect/jdbc/handling-complex-statements.md)|描述如何使用 JDBC 驅動程式來執行複雜陳述式，這類陳述式可執行各種不同的工作，並可能傳回不同類型的資料。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
