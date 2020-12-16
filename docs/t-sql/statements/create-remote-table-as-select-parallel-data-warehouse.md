---
description: CREATE REMOTE TABLE AS SELECT (平行處理資料倉儲)
title: CREATE REMOTE TABLE AS SELECT (平行處理資料倉儲)
ms.custom: seo-dt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
author: ronortloff
ms.author: rortloff
ms.reviewer: jrasnick
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: dc97f307022a28bcb2df00da4335c8676d32342f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471949"
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (平行處理資料倉儲)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫中選取資料，然後將該資料複製到遠端伺服器上 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的新資料表。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會使用具有所有 MPP 查詢處理優點的應用裝置，來選取要進行遠端複製的資料。 請將此用於需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的案例。  
  
 若要設定遠端伺服器，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Remote Table Copy＞(遠端資料表複製)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
CREATE REMOTE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }  AT ('<connection_string>')  
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
 要作為遠端資料表建立位置的資料庫。 *database_name* 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 預設值為目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上使用者登入的預設資料庫。  
  
 *schema_name*  
 新資料表的結構描述。 預設值為目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上使用者登入的預設結構描述。  
  
 *table_name*  
 新資料表的名稱。 如需有關所允許資料表名稱的詳細資料，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Object Naming Rules＞(物件命名規則)。  
  
 遠端資料表會建立成堆積。 其中不會包含檢查條件約束或觸發程序。 遠端資料表資料行的定序與來源資料表資料行的定序相同。 這適用於下列類型的資料行：**char**、**nchar**、**varchar** 及 **nvarchar**。  
  
 *connection_string*  
 指定用於連線至遠端伺服器和資料庫之 `Data Source`、`User ID` 及 `Password` 參數的字元字串。  
  
 連接字串是索引鍵與值組的清單 (以分號分隔)。 關鍵字不區分大小寫。 索引鍵與值組之間的空格會被忽略。 不過，視資料來源而定，值可能區分大小寫。  
  
 *資料來源*  
 指定遠端 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之名稱或 IP 位址及 TCP 連接埠號碼的參數。  
  
 *hostname* 或 *IP_address*  
 遠端伺服器電腦的名稱，或遠端伺服器的 IPv4 位址。 不支援 IPv6 位址。 您可以使用 **Computer_Name\Instance_Name** 或 **IP_address\Instance_Name** 格式來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體。 伺服器必須是遠端伺服器，因此不能指定為 (local)。  
  
 TCP *port* number  
 用於連線的 TCP 連接埠號碼。 針對不是在預設連接埠 1433 上進行接聽的 SQL Server 執行個體，您可以指定 0 到 65535 的 TCP 連接埠號碼。 例如：**ServerA,1450** 或 **10.192.14.27,1435**  
  
> [!NOTE]  
>  建議您使用 IP 位址來連線到遠端伺服器。 視您的網路組態而定，使用電腦名稱來進行連線可能需要額外的步驟，才能使用您的非應用裝置 DNS 伺服器將名稱解析成正確的伺服器。 使用 IP 位址來進行連線時，則不需要此步驟。 如需詳細資訊，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Use a DNS Forwarder to Resolve Non-Appliance DNS Names (Analytics Platform System)＞(使用 DNS 轉寄站來解析非應用裝置 DNS 名稱 (Analytics Platform System))。  
  
 *user_name*  
 有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入名稱。 字元數目上限是 128。  
  
 *password*  
 登入密碼。 字元數目上限是 128。  
  
 *batch_size*  
 每個批次的資料列數目上限。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會將資料列分批傳送至目的地伺服器。 *Batch_size* 是一個大於等於 0 的正整數。 預設值為 0。  
  
 WITH *common_table_expression*  
 指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 如需詳細資訊，請參閱 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)。  
  
 SELECT \<select_criteria> 指定哪些資料將填入新遠端資料表的查詢述詞。 如需 SELECT 陳述式的相關資訊，請參閱 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要：  
  
-   SELECT 子句中每個物件的 SELECT 權限。  
  
-   需要目的地 SMP 資料庫的 CREATE TABLE 權限。  
  
-   需要目的地 SMP 資料庫的 ALTER、INSERT 及 SELECT 權限。  
  
## <a name="error-handling"></a>錯誤處理  
 如果將資料複製到遠端資料庫失敗，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將會中止作業、記錄錯誤，然後嘗試刪除遠端資料表。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不保證能成功清除新資料表。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **遠端目的地伺服器**：  
  
-   針對連線到遠端伺服器，TCP 是預設且唯一支援的通訊協定。  
  
-   目的地伺服器必須是非應用裝置伺服器。 CREATE REMOTE TABLE 無法用來將資料從一個應用裝置複製到另一個應用裝置。  
  
-   CREATE REMOTE TABLE 陳述式只會建立新資料表。 因此，新資料表不可以是已經存在的資料表。 遠端資料庫和結構描述則必須已經存在。  
  
-   遠端伺服器必須有可用的空間，以儲存從應用裝置傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端資料庫的資料。  
  
 **SELECT 陳述式**：  
  
-   選取準則中不支援 ORDER BY 和 TOP 子句。  
  
-   CREATE REMOTE TABLE 無法在作用中的交易內執行，或在工作階段的 AUTOCOMMIT OFF 設定為作用中時執行。  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) 對此陳述式沒有任何作用。 若要達到類似的行為，請使用 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)。  
  
## <a name="locking-behavior"></a>鎖定行為  
 建立遠端資料表之後，必須等到開始進行複製，才會鎖定目的地資料表。 因此，在遠端資料表建立後到複製開始前，另一個程序有可能刪除遠端資料表。 當發生這種情況時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會產生錯誤，而複製則會失敗。  
  
## <a name="metadata"></a>中繼資料  
 請使用 [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) 來檢視將所選資料複製到遠端 SMP 伺服器的進度。 類型為 PARALLEL_COPY_READER 的資料列會包含此資訊。  
  
## <a name="security"></a>安全性  
 CREATE REMOTE TABLE 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連線到遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體；不會使用 Windows 驗證。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]對外網路必須使用防火牆，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接埠、系統管理連接埠及管理連接埠除外。  
  
 為了協助防止意外的資料遺失或損毀，用來從應用裝置複製到目的地資料庫的使用者帳戶應該只具備目的地資料庫的最低必要權限。  
  
 連線設定可讓您在連線到 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，使用 SSL 來保護使用者名稱和密碼資料，但實際資料則會以未加密的純文字形式傳送。 當發生這種情況時，惡意使用者可能會攔截 CREATE REMOTE TABLE 陳述式文字，其中包含用來登入 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱和密碼。 為了避免這個風險，請在對 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連線上使用資料加密。  
  
##  <a name="examples"></a><a name="Examples"></a> 範例  
  
### <a name="a-creating-a-remote-table"></a>A. 建立遠端資料表  
 此範例會在資料庫 `OrderReporting` 和結構描述 `Orders` 上建立一個名為 `MyOrdersTable` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP 遠端資料表。 `OrderReporting` 資料庫位於名為 `SQLA` 並在預設連接埠 1433 上進行接聽的伺服器上。 對該伺服器的連線會使用使用者 `David` 的認證，其密碼為 `e4n8@3`。  
  
```sql  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdm_pdw_dms_workers-dmv-for-remote-table-copy-status"></a>B. 查詢 sys.dm_pdw_dms_workers DMV 以了解遠端資料表複製狀態  
 此查詢示範如何檢視遠端資料表複製的複製狀態。  
  
```sql  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. 搭配 CREATE REMOTE TABLE 使用查詢聯結提示  
 此查詢示範搭配 CREATE REMOTE TABLE 使用查詢聯結提示的基本語法。 向控制節點提交查詢之後，在計算節點上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在產生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢計劃時套用雜湊聯結策略。 如需有關聯結提示及如何使用 OPTION 子句的詳細資訊，請參閱 [OPTION 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)。  
  
```sql  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

