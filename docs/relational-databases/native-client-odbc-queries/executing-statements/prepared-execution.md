---
title: 已準備好的執行 |微軟文件
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8265ed80028d5d8ac9696853a29474552f401f3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297915"
---
# <a name="prepared-execution"></a>備妥的執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC API 會定義備妥的執行，將它當做減少與重複執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式有關之剖析和編譯負擔的一個方式。 應用程式會建立一個包含 SQL 陳述式的字元字串，然後在兩個階段執行此字串。 它呼叫[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)一次,由分析敘述並將編譯為[!INCLUDE[ssDE](../../../includes/ssde-md.md)]執行計畫 。 然後,它調用**SQLExecute**執行,每次執行準備好的執行計劃。 這樣會省下每次執行時的剖析和編譯負擔。 應用程式通常會使用備妥的執行來重複執行相同且參數化的 SQL 陳述式。  
  
 對於大多數的資料庫而言，備妥的執行要比直接執行已執行三次或四次的陳述式更為快速，主要是因為該陳述式只會編譯一次，而直接執行的陳述式則會在每次執行時進行編譯。 備妥的執行也可以讓網路流量減少，因為每次執行該陳述式時，此驅動程式都可以將執行計畫識別碼和參數值 (而非整個 SQL 陳述式) 傳送給資料來源。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通過改進的演算法來檢測和重用**SQLExecDirect**的執行計畫,減少了直接執行和準備執行之間的性能差異。 如此可讓備妥的執行得到的某些效能優點可供直接執行的陳述式使用。 有關詳細資訊,請參閱[直接執行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 還會針對備妥的執行提供原生支援。 執行計畫建立在**SQLPrepare**上,後來在調用**SQLExecute**時執行。 由於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不需要在**SQLPrepare**上構建暫存記憶體,因此**在 tempdb**中的系統表上沒有額外的開銷。  
  
 出於性能原因,語句準備將延遲到調用**SQLExecute**或執行元屬性操作(如 ODBC 中的[SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)或[SQLDescribeParam)。](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) 此為預設行為。 要等到執行此陳述式或執行中繼屬性作業之後，才可得知正在準備之陳述式中的任何錯誤。 將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式特有的陳述式屬性 SQL_SOPT_SS_DEFER_PREPARE 設定為 SQL_DP_OFF 可以關閉這項預設行為。  
  
 在延遲準備的情況下,在調用**SQLExecute**之前調用**SQLDescribeCol**或**SQLDescribeParam**將生成額外的伺服器往返行程。 在**SQLDescribeCol**上,驅動程式從查詢中刪除 WHERE 子句,並將其發送到具有 SET FMTONLY ON 的伺服器,以獲取有關查詢返回的第一個結果集中列的說明。 在**SQLDescribeParam**上,驅動程式呼叫伺服器來取得查詢中任何參數標記引用的運算式或列的說明。 這個方法也有一些限制，例如無法解析子查詢中的參數。  
  
 對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式過度使用**SQLPrepare**會降低性能,尤其是在連接到早期版本的SQL Server時。 備妥的執行不應該用於單次執行的陳述式。 備妥的執行要比直接執行單次執行的陳述式更緩慢，因為它需要從用戶端到伺服器的額外網路往返。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上，它也會產生暫存預存程序。  
  
 準備陳述式無法用來在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上建立暫存物件。  
  
 一些早期的 ODBC 應用程式在使用[SQLBind 參數](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)時都使用**SQLPrepare。** **SQLBind參數**不需要使用**SQLPrepare,** 它可以與**SQLExecDirect**一起使用。 例如,將**SQLExecDirect**與**SQLBind 參數**一起從僅執行一次的儲存過程中檢索返回代碼或輸出參數。 除非將多次執行同一語句,否則不要將**SQLPrepare**與**SQLBind 參數**一起使用。  
  
## <a name="see-also"></a>另請參閱  
 [執行宣告&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
