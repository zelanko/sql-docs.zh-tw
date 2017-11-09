---
title: "建立遠端 TABLE AS SELECT (Parallel Data Warehouse) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0318d108d6dfaaa374af9a1ab8a148ff960dfcd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>建立遠端 TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  選取的資料從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫，並將該資料複製到新的資料表中的 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端伺服器上的資料庫。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置中，會使用 MPP 查詢處理，以選取的遠端副本資料的所有優點。 使用這項功能需要的案例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能。  
  
 若要設定遠端伺服器，請參閱 「 遠端資料表複製 」 中的[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要建立遠端資料表中的資料庫。 *database_name*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 預設值是在目的地上的使用者登入的預設資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
 *schema_name*  
 新資料表的結構描述。 預設值是在目的地上的使用者登入的預設結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
 *table_name*  
 新的資料表名稱。 如需詳細資訊允許資料表名稱，請參閱 < 物件命名規則 > 中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 建立遠端資料表為堆積。 它沒有 check 條件約束或觸發程序。 遠端資料表資料行的定序時的來源資料表資料行的定序相同。 這適用於類型的資料行**char**， **nchar**， **varchar**，和**nvarchar**。  
  
 *connection_string*  
 指定的字元字串`Data Source`， `User ID`，和`Password`連接到遠端伺服器和資料庫的參數。  
  
 連接字串會是索引鍵 / 值組的分號分隔清單。 關鍵字不區分大小寫。 索引鍵和值組之間的空格會被忽略。 不過，值可能會區分大小寫，視資料來源。  
  
 *資料來源*  
 參數指定的名稱或 IP 位址和 TCP 連接埠號碼為遠端 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 *主機名稱*或*IP_address*  
 遠端伺服器電腦或遠端伺服器的 IPv4 位址的名稱。 不支援 IPv6 位址。 您可以指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具名執行個體的格式**Computer_Name\Instance_Name**或**IP_address\Instance_Name**。 伺服器必須是遠端，因此不能指定為 (local)。  
  
 TCP*連接埠*數目  
 連線的 TCP 通訊埠編號。 您可以指定 TCP 通訊埠編號從 0 到 65535 之間未接聽預設通訊埠 1433年的 SQL Server 執行個體。 例如： **ServerA，1450年**或**10.192.14.27,1435**  
  
> [!NOTE]  
>  我們建議使用的 IP 位址連接到遠端伺服器。 根據您的網路設定，使用電腦名稱來連線可能需要其他步驟，以使用您非應用裝置的 DNS 伺服器解析至正確的伺服器名稱。 使用 IP 位址進行連接時，不需要此步驟。 如需詳細資訊，請參閱 「 使用 DNS 轉寄站來解析非應用裝置的 DNS 名稱 (Analytics Platform System) 」，在[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 *user_name*  
 有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入名稱。 字元數上限為 128。  
  
 *密碼*  
 登入密碼。 字元數上限為 128。  
  
 *batch_size*  
 每個批次的資料列的數目上限。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將批次中的資料列傳送到目的地伺服器。 *Batch_size*這是一個正整數 > = 0。 預設值為 0。  
  
 與*common_table_expression*  
 指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 如需詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 選取\<select_criteria > 指定的資料將會填入新的遠端資料表的查詢述詞。 在 SELECT 陳述式上的資訊，請參閱[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要：  
  
-   SELECT 子句中的每個物件上的 SELECT 權限。  
  
-   需要目的地 SMP 資料庫上的 CREATE TABLE 權限。  
  
-   需要 ALTER、 INSERT 和 SELECT 權限目的 SMP 結構描述。  
  
## <a name="error-handling"></a>錯誤處理  
 如果將資料複製到遠端資料庫失敗，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會中止作業中，記錄錯誤，並嘗試刪除遠端資料表。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不保證成功清除的新資料表。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **遠端目的伺服器**:  
  
-   TCP 是預設值，只支援通訊協定連線到遠端伺服器。  
  
-   目的地伺服器必須是在非應用裝置的伺服器。 CREATE REMOTE TABLE 無法用來將資料從一個工具複製到另一個。  
  
-   CREATE REMOTE TABLE 陳述式只會建立新的資料表。 因此，新的資料表不存在。 遠端資料庫和結構描述必須已經存在。  
  
-   遠端伺服器必須有可用的應用裝置，以傳輸將資料儲存空間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端資料庫。  
  
 **SELECT 陳述式**:  
  
-   不支援 ORDER BY 和 TOP 子句中的選取準則。  
  
-   無法執行 CREATE REMOTE TABLE，在使用中交易內，或當關閉自動認可設定為使用中工作階段。  
  
 [SET ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)此陳述式上沒有作用。 若要達成類似的行為，使用[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>鎖定行為  
 建立遠端資料表之後, 目標資料表未鎖定複製開始之前。 因此，它可能會刪除遠端資料表建立之後，複製開始之前，另一個處理序。 當發生這種情況時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會產生錯誤，而且複製會失敗。  
  
## <a name="metadata"></a>中繼資料  
 使用[sys.dm_pdw_dms_workers &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)檢視進度，將選取的資料複製到遠端的 SMP 伺服器。 資料列型別 PARALLEL_COPY_READER 包含這項資訊。  
  
## <a name="security"></a>安全性  
 使用 CREATE REMOTE TABLE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證來連接到遠端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體; 它不會使用 Windows 驗證。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]外部對向網路必須啟用防火牆的連線，發生例外狀況的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接埠、 系統管理的連接埠和管理連接埠。  
  
 以協助防止資料意外遺失或損毀用來從工具複製到目的地資料庫的使用者帳戶應該在目的地資料庫上有只的最小的必要權限。  
  
 連接設定可讓您連接到 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 保護使用者名稱和密碼資料，但未加密的純文字傳送的實際資料的執行個體。 當發生這種情況時，惡意使用者能夠攔截 CREATE REMOTE TABLE 陳述式文字，其中包含[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者名稱和密碼登入 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 若要避免此風險，請使用資料加密 SMP 連接上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
##  <a name="Examples"></a> 範例  
  
### <a name="a-creating-a-remote-table"></a>A. 建立遠端資料表  
 這個範例會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SMP 遠端資料表稱為`MyOrdersTable`資料庫上`OrderReporting`和結構描述`Orders`。 `OrderReporting`資料庫是在名為的伺服器上`SQLA`預設通訊埠 1433年上接聽。 伺服器的連線會使用使用者的認證`David`，密碼是`e4n8@3`。  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. 查詢 sys.dm_pdw_dms_workers DMV 的遠端資料表複製狀態  
 此查詢會顯示如何檢視遠端資料表複製的複製狀態。  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. 使用 CREATE REMOTE TABLE 查詢聯結提示  
 此查詢會顯示使用 CREATE REMOTE TABLE 查詢聯結提示的基本語法。 查詢提送到的控制節點之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 計算節點上執行，會在產生時套用雜湊聯結策略[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢計劃。 如需有關聯結提示，以及如何使用 OPTION 子句的詳細資訊，請參閱[OPTION 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


