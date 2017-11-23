---
title: "SET 陳述式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET
- SET_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ISO SET statements
- queries [SQL Server], executing
- dates [SQL Server], SET statements
- time [SQL Server], SET statements
- SET statement, about SET statement
- SET statement
- statistical information [SQL Server], SET statements
- locking [SQL Server], SET statements
ms.assetid: f7e107f8-0fcf-408b-b30f-da2323eeb714
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3832a2be6952354122c999d3c88c7ad1610b623d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-statements-transact-sql"></a>SET 陳述式 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計語言提供了許多 SET 陳述式，供您變更目前工作階段對於特定資訊的處理。 這些 SET 陳述式可分組成下表所顯示的類別目錄。  
  
 設定本機變數的 SET 陳述式的相關資訊，請參閱[設定@local_variable&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
|類別目錄|陳述式|  
|--------------|----------------|  
|日期和時間陳述式|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)<br /><br /> [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|  
|鎖定陳述式|[SET DEADLOCK_PRIORITY](../../t-sql/statements/set-deadlock-priority-transact-sql.md)<br /><br /> [SET LOCK_TIMEOUT](../../t-sql/statements/set-lock-timeout-transact-sql.md)|  
|其他陳述式|[SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)<br /><br /> [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)<br /><br /> [SET FIPS_FLAGGER](../../t-sql/statements/set-fips-flagger-transact-sql.md)<br /><br /> [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)<br /><br /> [設定語言](../../t-sql/statements/set-language-transact-sql.md)<br /><br /> [組位移](../../t-sql/statements/set-offsets-transact-sql.md)<br /><br /> [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)|  
|查詢執行陳述式|[SET ARITHABORT](../../t-sql/statements/set-arithabort-transact-sql.md)<br /><br /> [SET ARITHIGNORE](../../t-sql/statements/set-arithignore-transact-sql.md)<br /><br /> [SET FMTONLY](../../t-sql/statements/set-fmtonly-transact-sql.md)<br /><br /> 注意：[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> [SET NOCOUNT](../../t-sql/statements/set-nocount-transact-sql.md)<br /><br /> [SET NOEXEC](../../t-sql/statements/set-noexec-transact-sql.md)<br /><br /> [SET NUMERIC_ROUNDABORT](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)<br /><br /> [SET PARSEONLY](../../t-sql/statements/set-parseonly-transact-sql.md)<br /><br /> [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)<br /><br /> [SET ROWCOUNT](../../t-sql/statements/set-rowcount-transact-sql.md)<br /><br /> [SET TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)|  
|ISO 設定陳述式|[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_OFF](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)<br /><br /> [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)<br /><br /> [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)<br /><br /> [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)|  
|統計資料陳述式|[SET FORCEPLAN](../../t-sql/statements/set-forceplan-transact-sql.md)<br /><br /> [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md)<br /><br /> [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md)<br /><br /> [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)<br /><br /> [SET STATISTICS IO](../../t-sql/statements/set-statistics-io-transact-sql.md)<br /><br /> [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)<br /><br /> [設定統計資料設定檔](../../t-sql/statements/set-statistics-profile-transact-sql.md)<br /><br /> [設定統計資料的時間](../../t-sql/statements/set-statistics-time-transact-sql.md)|  
|交易陳述式|[SET IMPLICIT_TRANSACTIONS](../../t-sql/statements/set-implicit-transactions-transact-sql.md)<br /><br /> [SET REMOTE_PROC_TRANSACTIONS](../../t-sql/statements/set-remote-proc-transactions-transact-sql.md)<br /><br /> [將交易隔離層級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)<br /><br /> [SET XACT_ABORT](../../t-sql/statements/set-xact-abort-transact-sql.md)|  
  
## <a name="considerations-when-you-use-the-set-statements"></a>SET 陳述式的使用考量  
  
-   所有 SET 陳述式都是在執行階段實作，但 SET FIPS_FLAGGER、SET OFFSETS、SET PARSEONLY 和 SET QUOTED_IDENTIFIER 除外。 這幾個陳述式是在剖析階段實作。  
  
-   如果在預存程序或觸發程序中執行 SET 陳述式，從預存程序或觸發程序傳回控制權之後，會還原 SET 選項的值。 此外，如果使用執行動態 SQL 字串中指定 SET 陳述式，則**sp_executesql**或從動態 SQL 字串中指定的批次傳回控制權之後，還原 EXECUTE，SET 選項的值。  
  
-   預存程序是利用執行階段所指定的 SET 設定 (除了 SET ANSI_NULLS 和 SET QUOTED_IDENTIFIER) 來執行的。 指定 SET ANSI_NULLS 或 SET QUOTED_IDENTIFIER 的預存程序會使用建立預存程序時所指定的設定。 如果用於預存程序內，任何 SET 設定都會被忽略。  
  
-   **使用者選項**設定**sp_configure**允許的全伺服器設定，且可運作的多個資料庫。 除了出現在登入階段之外，這項設定的行為也如同明確的 SET 陳述式。  
  
-   利用 ALTER DATABASE 來設定的資料庫設定，只在資料庫層級才有效，且只在明確設定時才有效。 資料庫設定會覆寫執行個體 選項設定的設定使用**sp_configure**。  
  
-   對於任何含有 ON 和 OFF 設定的 SET 陳述式，您都可以指定多個 SET 選項的 ON 或 OFF 設定。  
  
    > [!NOTE]  
    >  這並不適用於與統計資料相關的 SET 選項。  
  
     例如，`SET QUOTED_IDENTIFIER, ANSI_NULLS ON`將 QUOTED_IDENTIFIER 和 ANSI_NULLS 設為 ON。  
  
-   SET 陳述式設定會覆寫使用 ALTER DATABASE 所設定的對等資料庫選項設定。 例如，SET ANSI_NULLS 陳述式所指定的值會覆寫 ANSI_NULL 的資料庫設定。 此外，部份連接設定會自動設定在使用者連線至資料庫，根據先前使用的使生效的值時**sp_configure 使用者選項**設定或值套用至所有的 ODBC 和OLE DB 連接。  
  
-   ALTER、CREATE 和 DROP DATABASE 陳述式不接受 SET LOCK_TIMEOUT 設定。  
  
-   當全域或捷徑 SET 陳述式 (如 SET ANSI_DEFAULTS) 設定多項設定時，發出捷徑 SET 陳述式會重設捷徑 SET 陳述式影響所及的所有選項先前的設定。 如果在發出捷徑 SET 陳述式之後，才明確設定捷徑 SET 陳述式影響所及的個別 SET 選項，這個個別 SET 陳述式會覆寫對應的捷徑設定。  
  
-   當使用批次時，資料庫內容取決於利用 USE 陳述式建立的批次。 隨選查詢和在預存程序之外執行以及在批次中的所有其他陳述式，都繼承 USE 陳述式所建立之資料庫和連接的選項設定。  
  
-   Multiple Active Result Set (MARS) 要求會共用包含最新工作階段 SET 選項設定的全域狀態。 當執行各項要求時，它都能夠修改 SET 選項。 變更專屬於設定它們的要求內容，不會影響其他並行 MARS 要求。 不過，在要求執行完成之後，會將新的 SET 選項複製到全域工作階段狀態中。 在這項變更之後，相同工作階段所執行的新要求會使用這些新的 SET 選項設定。  
  
-   當執行預存程序時，不論是從批次執行，或另一個預存程序執行，都會利用這個預存程序所在資料庫中目前所設定的選項值來執行。 例如，當預存程序**db1.dbo.sp1**呼叫預存程序**db2.dbo.sp2**，預存程序**sp1**執行目前的相容性層級設定資料庫的**db1**，預存程序和**sp2**下的資料庫目前的相容性層級設定為執行**db2**。  
  
-   當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式參考在多個資料庫中的物件時，這個陳述式會套用目前的資料庫內容及目前的連接內容。 在這個情況下，如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式是在批次中，目前的連接內容就是 USE 陳述式所定義的資料庫；如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式是在預存程序中，連接內容就是預存程序所在的資料庫。  
  
-   當您建立和操作計算資料行索引或索引檢視時，ARITHABORT、CONCAT_NULL_YIELDS_NULL、QUOTED_IDENTIFIER、ANSI_NULLS、ANSI_PADDING 和 ANSI_WARNINGS 等 SET 選項都必須設成 ON。 NUMERIC_ROUNDABORT 選項必須設成 OFF。  
  
     如果任何這些選項未設成所需要的值，在索引檢視或含計算資料行索引的資料表上執行 INSERT、UPDATE、DELETE、DBCC CHECKDB 和 DBCC CHECKTABLE 動作都會失敗。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會產生一個錯誤，列出所有設定不正確的選項。 另外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會依照計算資料行或檢視的索引並不存在的方式，來處理這些資料表或索引檢視的 SELECT 陳述式。  
  
  
