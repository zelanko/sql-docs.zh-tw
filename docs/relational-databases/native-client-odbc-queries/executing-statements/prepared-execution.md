---
title: "備妥的執行 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cedfb3926904af0a9d7393a1ff896c3c2f08a61f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="prepared-execution"></a>備妥的執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC API 會定義備妥的執行，將它當做減少與重複執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式有關之剖析和編譯負擔的一個方式。 應用程式會建立一個包含 SQL 陳述式的字元字串，然後在兩個階段執行此字串。 它會呼叫[SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)一次陳述式剖析和編譯成執行計畫[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 然後它會呼叫**SQLExecute**每次執行已備妥的執行計畫。 這樣會省下每次執行時的剖析和編譯負擔。 應用程式通常會使用備妥的執行來重複執行相同且參數化的 SQL 陳述式。  
  
 對於大多數的資料庫而言，備妥的執行要比直接執行已執行三次或四次的陳述式更為快速，主要是因為該陳述式只會編譯一次，而直接執行的陳述式則會在每次執行時進行編譯。 備妥的執行也可以讓網路流量減少，因為每次執行該陳述式時，此驅動程式都可以將執行計畫識別碼和參數值 (而非整個 SQL 陳述式) 傳送給資料來源。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會減少直接執行與備妥執行透過改良過的演算法來偵測及重複使用執行計畫的效能差異**SQLExecDirect**。 如此可讓備妥的執行得到的某些效能優點可供直接執行的陳述式使用。 如需詳細資訊，請參閱[直接執行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 還會針對備妥的執行提供原生支援。 執行計畫建立在**SQLPrepare**和更新版本時執行**SQLExecute**呼叫。 因為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立暫存預存程序不需要**SQLPrepare**中的系統資料表中沒有額外負擔**tempdb**。  
  
 基於效能考量，陳述式準備會延遲，直到**SQLExecute**稱為或中繼屬性作業 (例如[SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)或[SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) ODBC 中) 會執行。 這是預設行為。 要等到執行此陳述式或執行中繼屬性作業之後，才可得知正在準備之陳述式中的任何錯誤。 將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式特有的陳述式屬性 SQL_SOPT_SS_DEFER_PREPARE 設定為 SQL_DP_OFF 可以關閉這項預設行為。  
  
 是延遲的準備，呼叫**SQLDescribeCol**或**SQLDescribeParam**之前先呼叫**SQLExecute**會產生額外往返伺服器。 在**SQLDescribeCol**，驅動程式會移除查詢的 WHERE 子句，並傳送到伺服器時使用 SET FMTONLY ON 中第一個查詢所傳回的結果集取得資料行的描述。 在**SQLDescribeParam**，驅動程式會呼叫伺服器以取得運算式或查詢中的任何參數標記所參考的資料行的描述。 這個方法也有一些限制，例如無法解析子查詢中的參數。  
  
 過度使用**SQLPrepare**與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會降低效能，尤其是連接到舊版 SQL Server。 備妥的執行不應該用於單次執行的陳述式。 備妥的執行要比直接執行單次執行的陳述式更緩慢，因為它需要從用戶端到伺服器的額外網路往返。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上，它也會產生暫存預存程序。  
  
 準備陳述式無法用來在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上建立暫存物件。  
  
 某些早期的 ODBC 應用程式使用**SQLPrepare**隨時[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)所使用。 **SQLBindParameter**不需要使用**SQLPrepare**，它可以搭配**SQLExecDirect**。 例如，使用**SQLExecDirect**與**SQLBindParameter**擷取傳回碼或輸出參數，系統只會執行一次預存程序。 請勿使用**SQLPrepare**與**SQLBindParameter**除非相同的陳述式執行多次。  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
