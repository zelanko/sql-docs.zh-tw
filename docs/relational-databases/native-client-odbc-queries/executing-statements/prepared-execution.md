---
description: 備妥的執行
title: 備妥的執行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a2fbc7fe209653a142ea887999fc95310f29e30b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438351"
---
# <a name="prepared-execution"></a>備妥的執行
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC API 會定義備妥的執行，將它當做減少與重複執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式有關之剖析和編譯負擔的一個方式。 應用程式會建立一個包含 SQL 陳述式的字元字串，然後在兩個階段執行此字串。 它會呼叫 [SQLPrepare 函數](../../../odbc/reference/syntax/sqlprepare-function.md) 一次，以將語句剖析及編譯成執行計畫 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 。 然後，它會在每次執行已備妥的執行計畫時，呼叫 **SQLExecute** 。 這樣會省下每次執行時的剖析和編譯負擔。 應用程式通常會使用備妥的執行來重複執行相同且參數化的 SQL 陳述式。  
  
 對於大多數的資料庫而言，備妥的執行要比直接執行已執行三次或四次的陳述式更為快速，主要是因為該陳述式只會編譯一次，而直接執行的陳述式則會在每次執行時進行編譯。 備妥的執行也可以讓網路流量減少，因為每次執行該陳述式時，此驅動程式都可以將執行計畫識別碼和參數值 (而非整個 SQL 陳述式) 傳送給資料來源。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 透過經過改良的演算法來偵測及重複使用 **SQLExecDirect** 中的執行計畫，以降低直接和準備執行之間的效能差異。 如此可讓備妥的執行得到的某些效能優點可供直接執行的陳述式使用。 如需詳細資訊，請參閱 [直接執行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 還會針對備妥的執行提供原生支援。 執行計畫是以 **SQLPrepare** 為基礎建立的，稍後在呼叫 **SQLExecute** 時執行。 因為不 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要在 **SQLPrepare** 上建立暫存預存程序，所以 **tempdb** 中的系統資料表沒有額外的額外負荷。  
  
 基於效能考慮，語句準備會延遲，直到呼叫 **SQLExecute** ，或執行中繼屬性作業 (例如 [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) 或 [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) in ODBC) 。 這是預設行為。 要等到執行此陳述式或執行中繼屬性作業之後，才可得知正在準備之陳述式中的任何錯誤。 將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式特有的陳述式屬性 SQL_SOPT_SS_DEFER_PREPARE 設定為 SQL_DP_OFF 可以關閉這項預設行為。  
  
 如果是延後準備，呼叫 **SQLDescribeCol** 或 **SQLDescribeParam** ，然後再呼叫 **SQLExecute** ，就會產生額外的伺服器往返。 在 **SQLDescribeCol** 上，驅動程式會從查詢中移除 WHERE 子句，並使用 SET FMTONLY ON 將它傳送至伺服器，以取得查詢所傳回之第一個結果集的資料行描述。 在 **SQLDescribeParam** 上，驅動程式會呼叫伺服器來取得查詢中任何參數標記所參考的運算式或資料行的描述。 這個方法也有一些限制，例如無法解析子查詢中的參數。  
  
 與 Native Client ODBC 驅動程式過度搭配使用 **SQLPrepare** 會 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 降低效能，特別是當連接到舊版的 SQL Server 時。 備妥的執行不應該用於單次執行的陳述式。 備妥的執行要比直接執行單次執行的陳述式更緩慢，因為它需要從用戶端到伺服器的額外網路往返。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上，它也會產生暫存預存程序。  
  
 準備陳述式無法用來在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上建立暫存物件。  
  
 某些早期 ODBC 應用程式使用 **SQLPrepare** 任何時間 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 。 **SQLBindParameter** 不需要使用 **SQLPrepare**，它可以搭配 **SQLExecDirect** 使用。 例如，使用 **SQLExecDirect** 搭配 **SQLBindParameter** ，從只執行一次的預存程式取出傳回碼或輸出參數。 請勿使用 **SQLPrepare** 搭配 **SQLBindParameter** ，除非相同的語句會執行多次。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行語句 ](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
