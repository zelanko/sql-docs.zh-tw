---
title: 不可部分完成的區塊 | Microsoft Docs
description: 深入了解 BEGIN ATOMIC；這是 ANSI SQL 標準的一部分。 SQL Server 支援原生程序中的 ATOMIC 區塊。
ms.custom: ''
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e92f73b4f8790c80cf0ac4e790a0587593ac75e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537724"
---
# <a name="atomic-blocks-in-native-procedures"></a>原生程序中不可部分完成的區塊
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **BEGIN ATOMIC** 是 ANSI SQL 標準的一部分。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援原生編譯之預存程序最上層的 ATOMIC 區塊，以及原生編譯之純量使用者定義函式的 ATOMIC 區塊。 如需這些函數的詳細資訊，請參閱 [記憶體內部 OLTP 的純量使用者定義函數](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
-   每個原生編譯預存程序剛好包含一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式區塊。 這是 ATOMIC 區塊。  
  
-   非原生、解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序和隨選批次不支援不可部分完成的區塊。  
  
 不可部分完成的區塊會在交易內執行 (以不可分割方式)。 區塊中的所有陳述式將會成功，或是整個區塊將會回復到區塊開頭所建立的儲存點。 此外，對於不可部分完成的區塊而言，工作階段設定是固定的。 在工作階段中以不同設定執行相同的不可部分完成的區塊將會產生相同的行為，與目前工作階段的設定無關。  
  
## <a name="transactions-and-error-handling"></a>交易和錯誤處理  
 如果交易已經存在於工作階段 (因為執行 **BEGIN TRANSACTION** 陳述式的批次和交易依然使用中)，則啟動 ATOMIC 區塊將會在交易中建立儲存點。 如果區塊結束而沒有發生例外狀況，則會認可針對區塊建立的儲存點，但在工作階段層級的交易認可之前不會認可交易。 如果區塊擲回例外狀況，則會回復區塊的作用，但是工作階段層級的交易將會繼續，除非例外狀況讓交易毀滅。 例如，寫入衝突將會毀滅交易，但類型轉換錯誤則不會。  
  
 如果工作階段上沒有使用中交易， **BEGIN ATOMIC** 將會開始新的交易。 如果區塊範圍之外未擲回任何例外狀況，此交易將會在區塊結尾認可。 如果區塊擲回例外狀況 (也就是說，未在區塊內捕捉及處理例外狀況)，交易將會回復。 如果交易橫跨單一 ATOMIC 區塊 (單一原生編譯的預存程序)，您就不需要撰寫明確的 **BEGIN TRANSACTION** 和 **COMMIT** 或 **ROLLBACK** 陳述式。  
  
 原生編譯的預存程序支援 **TRY**、 **CATCH**和 **THROW** 建構用於錯誤處理。 不支援**RAISERROR** 。  
  
 下列範例說明使用不可部分完成的區塊和原生編譯預存程序處理錯誤的行為：  
  
```sql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 記憶體最佳化資料表特有的以下錯誤訊息會毀滅交易。 如果它們發生在不可部分完成的區塊範圍內，將造成交易中止：10772、41301、41302、41305、41325、41332、41333 及 41839。  
  
## <a name="session-settings"></a>工作階段設定  
 當編譯預存程序時，將會修復不可部分完成的區塊內的工作階段設定。 某些設定可以使用 **BEGIN ATOMIC** 來指定，而其他設定則一律固定為相同的值。  
  
 **BEGIN ATOMIC**需要以下選項：  
  
|必要設定|描述|  
|----------------------|-----------------|  
|**TRANSACTION ISOLATION LEVEL**|支援的值為 **SNAPSHOT**、 **REPEATABLEREAD**和 **SERIALIZABLE**。|  
|**LANGUAGE**|判斷日期和時間格式及系統訊息。 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 中的所有語言和別名都受到支援。|  
  
 以下是選擇性設定：  
  
|選擇性設定|描述|  
|----------------------|-----------------|  
|**DATEFORMAT**|所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期格式都受到支援。 當指定時， **DATEFORMAT** 會覆寫與 **LANGUAGE**相關聯的預設日期格式。|  
|**DATEFIRST**|當指定時， **DATEFIRST** 會覆寫與 **LANGUAGE**相關聯的預設值。|  
|**DELAYED_DURABILITY**|支援的值為 **OFF** 和 **ON**。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易認可可能是完全持久、預設值或延遲的持久。如需詳細資訊，請參閱[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)。|  
  
 對於所有原生編譯預存程序中所有不可部分完成的區塊，下列 SET 選項都有相同的系統預設值：  
  
|Set 選項|不可部分完成的區塊的系統預設值|  
|----------------|--------------------------------------|  
|ANSI_NULLS|開啟|  
|ANSI_PADDING|開啟|  
|ANSI_WARNING|開啟|  
|ARITHABORT|開啟|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|開啟|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|開啟|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|開啟|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> 未捕捉到的例外狀況會造成不可部分完成的區塊回復，但是並不會造成交易中止，除非錯誤會毀滅交易。|  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
