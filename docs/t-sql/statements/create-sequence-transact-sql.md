---
title: "建立順序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a96d101c17f528b9ff14ca523e5dc41ada2f4c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  建立順序物件，並指定其屬性。 序列是使用者定義之結構描述繫結的物件，該物件會根據建立序列所使用的規格產生一連串的數值。 數值序列會在定義的間隔依照遞增或遞減順序來產生，而且在用完時可設定為重新啟動 (循環)。 順序不會與特定資料表產生關聯，與識別欄位不同。 應用程式會參考順序物件，以擷取它的下一個值。 順序與資料表之間的關聯性是由應用程式所控制。 使用者的應用程式可以參考序列物件，並協調跨越多個資料列和資料表的值。  
  
 不同於插入資料列時，會產生的識別資料行值，應用程式可以取得下一個序號而不需要插入資料列，藉由呼叫[NEXT VALUE FOR 函數](../../t-sql/functions/next-value-for-transact-sql.md)。 您可以使用 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 一次取得多個序號。  
  
 如需使用 **CREATE SEQUENCE** 和 **NEXT VALUE FOR** 函數的相關資訊和案例，請參閱 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *sequence_name*  
 指定資料庫中順序的唯一識別名稱。 型別是**sysname**。  
  
 [ built_in_integer_type | user-defined_integer_type  
 順序可以定義為任何整數類型。 允許使用下列類型。  
  
-   **tinyint** -0 到 255 範圍  
  
-   **smallint** -範圍-32,768 到 32,767  
  
-   **int** -範圍介於-2,147,483,648 到 2,147,483,647  
  
-   **bigint** -範圍是-9223372036854775808 到 9,223,372,036,854,775,807  
  
-   **十進位**和**數值**小數位數為 0。  
  
-   以其中一個允許類型為基礎的任何使用者定義的資料類型 (別名類型)。  
  
 如果未不提供任何資料類型，則**bigint**預設會使用資料型別。  
  
 START WITH\<常數 >  
 順序物件傳回的第一個值。 **啟動**值必須小於或等於最大而且大於或等於順序物件的最小值。 新順序物件的預設開始值是遞增順序物件的最小值，是遞減順序物件的最大值。  
  
 遞增的\<常數 >  
 用來遞增 （遞減如果是負數） 的值每次呼叫的順序物件的值**NEXT VALUE FOR**函式。 如果增量是負值，則會遞減順序物件，否則會遞增。 增量不能為 0。 新順序物件的預設增量為 1。  
  
 [MINVALUE\<常數 > |**沒有 MINVALUE** ]  
 指定順序物件的界限。 新序列物件的預設最小值是序列物件之資料類型的最小值。 如果是 **tinyint** 資料類型，這是零，如果是所有其他資料類型，則為負數。  
  
 [MAXVALUE\<常數 > |**沒有 MAXVALUE**  
 指定順序物件的界限。 新序列物件的預設最大值是序列物件之資料類型的最大值。  
  
 [循環 |**NO CYCLE** ]  
 屬性，指定當超出其最小值或最大值時，順序物件應該從最小值 (或是遞減順序物件的最大值) 重新啟動，還是擲回例外狀況。 新順序物件的預設循環選項是 NO CYCLE。  
  
 請注意，循環是從最小值或最大值重新啟動，而不是從開始值重新啟動。  
  
 [**快取**[\<常數 >] |無快取]  
 藉由減少產生序號所需的磁碟 IO 數目，對使用順序物件的應用程式提升效能。 預設為 CACHE。  
  
 例如，如果選擇的快取大小為 50，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會保留快取的 50 個個別值。 它只快取目前值和留在快取中的值數目。 這表示，儲存快取所需的記憶體數量永遠是順序物件之資料類型的兩個執行個體。  
  
> [!NOTE]  
>  如果已啟用快取選項但未指定快取大小，Database Engine 將選取大小。 但是使用者不應該依賴此選取來取得一致的結果。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 可能變更計算快取大小的方法，而不另行通知。  
  
 使用建立時**快取**選項時，非預期的關閉 （例如停電） 可能會導致的快取中剩餘的序號遺失。  
  
## <a name="general-remarks"></a>一般備註  
 序號是在目前交易範圍之外產生的。 無論使用序號的交易被認可或回復交易，都會耗用序號。  
  
### <a name="cache-management"></a>快取管理  
 為了改善效能，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預先配置所指定的序號數目**快取**引數。  
  
 例如，建立起始值為 1 和快取大小為 15 的新順序。 當需要第一個值時，會從記憶體中提供 1 到 15 的值。 最後一個快取的值 (15) 會寫入至磁碟上的系統資料表。 已使用所有 15 個數字時，下一個要求 (針對數字 16) 將會造成快取重新配置。 新的最後一個快取值 (30) 會寫入至系統資料表。  
  
 如果在您使用 22 個數字之後 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 停止，記憶體中的下一個預定序號 (23) 會寫入至系統資料表，取代先前儲存的數字。  
  
 在 SQL Server 重新啟動，而且需要一個序號之後，會從系統資料表讀取起始數字 (23)。 15 個數字 (23-38) 的快取數量會配置到記憶體，而且下一個非快取數字 (39) 會寫入至系統資料表。  
  
 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]停電等事件的異常停止，順序會重新啟動與從系統資料表 (39) 的讀取數。 任何一串數字配置到記憶體 （但永遠不會要求使用者或應用程式） 都會遺失。 這項功能可能會留下間距，但保證相同的值將永遠不會發行兩次的單一順序物件，除非它定義為**循環**或手動重新啟動。  
  
 快取是透過追蹤目前值 (最後一個發出的值) 以及留在快取中的值數目，保留在記憶體中。 因此，快取所使用的記憶體數量永遠是順序物件之資料類型的兩個執行個體。  
  
 快取引數設定為**NO CACHE**系統資料表使用順序時會每次寫入目前的順序值。 這可能會因為增加磁碟的存取而降低效能，但是可以減少非預期間距的機會。 如果要求使用數字，仍然會發生間距**NEXT VALUE FOR**或**sp_sequence_get_range**函式，但接著數字未使用或用於未認可的交易。  
  
 當順序物件使用**快取**選項時，如果您重新啟動順序物件，或改變**遞增**，**循環**， **MINVALUE**，**MAXVALUE**，或快取大小屬性，它就會導致系統資料表發生變更之前寫入快取。 然後快取會從目前的值開始重新載入 (也就是不略過任何數字)。 快取大小的變更會立即生效。  
  
 **快取的值可用時的 CACHE 選項**  
  
 下列程序每次要求順序物件產生的下一個值**快取**選項如果順序物件的記憶體中快取中有未使用的值。  
  
1.  計算順序物件的下一個值。  
  
2.  更新記憶體中順序物件的新的目前值。  
  
3.  將計算值傳回給呼叫的陳述式。  
  
 **快取已用盡時，會產生快取選項。**  
  
 每次要求順序物件產生的下一個值，就會發生下列處理序**快取**快取已用盡選項：  
  
1.  計算順序物件的下一個值。  
  
2.  計算新快取的最後一個值。  
  
3.  鎖定順序物件的系統資料表資料列，而且將步驟 2 中的計算值 (最後一個值) 寫入至系統資料表。 引發快取用盡 xevent，通知使用者此新持續值。  
  
 **NO CACHE 選項**  
  
 下列程序每次要求順序物件產生的下一個值**NO CACHE**選項：  
  
1.  計算順序物件的下一個值。  
  
2.  將順序物件的新的目前值寫入至系統資料表。  
  
3.  將計算值傳回給呼叫的陳述式。  
  
## <a name="metadata"></a>中繼資料  
 如需有關順序的詳細資訊，請查詢 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要 SCHEMA 的 **CREATE SEQUENCE**、 **ALTER**或 **CONTROL** 權限。  
  
-   Db_owner 和 db_ddladmin 固定資料庫角色的成員可以建立、 改變和卸除順序物件。  
  
-   Db_owner 和 db_datawriter 固定資料庫角色的成員，讓它們產生數字，藉以更新順序物件。  
  
 下列範例會授與使用者 AdventureWorks\Larry 權限，以測試結構描述中建立的序列。  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 順序物件的擁有權可以傳送使用**ALTER AUTHORIZATION**陳述式。  
  
 如果順序使用使用者定義的資料類型，順序的建立者必須擁有類型的 REFERENCES 權限。  
  
### <a name="audit"></a>稽核  
 若要稽核**CREATE SEQUENCE**，監視**SEQUENCE&LT;**。  
  
## <a name="examples"></a>範例  
 如需建立順序和使用的範例**NEXT VALUE FOR**函數產生序號，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 大部分的下列範例會在名為 Test 的結構描述中建立順序物件。  
  
 若要建立測試結構描述，請執行下列陳述式。  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. 建立以 1 遞增的順序  
 在下列範例中，Thierry 會建立一個中名為遞增的 CountBy1，每次使用它時的順序。  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. 建立以 1 遞減的順序  
 下列範例會從 0 開始，並且每次使用時遞減一。  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. 建立以 5 遞增的順序  
 下列範例會建立每次使用時遞增 5 的順序。  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. 建立以指定數字開頭的順序  
 在匯入資料表之後，Thierry 發現使用的最高識別碼值是 24,328。 Thierry 需要產生以 24,329 為起始值的順序。 下列程式碼會建立開頭為 24,329 且遞增量為 1 的順序。  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. 建立使用預設值的順序  
 下列範例會建立使用預設值的順序。  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 執行下列陳述式，以檢視順序的屬性。  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 輸出的部分清單示範預設值。  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. 建立具有特定資料類型的順序  
 下列範例會建立序列使用**smallint**資料型別，以及範圍從-32,768 到 32,767。  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. 建立使用所有引數的順序  
 下列範例會建立名為 DecSeq 使用序列**十進位**具備範圍從 0 到 255 之間的資料類型。 順序開頭為 125，而且每次產生數字時會遞增 25。 因為順序設定為循環，所以當值超過最大值 200 時，順序會從最小值 100 重新啟動。  
  
```  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 執行下列陳述式以查看第一個值，即值為 125 的 `START WITH` 選項。  
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 再執行陳述式三次，以傳回 150、175 和 200。  
  
 重新執行陳述式，以查看開始值循環回到 `MINVALUE` 選項值 100。  
  
 執行下列程式碼，以確認快取大小，並查看目前的值。  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SEQUENCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [卸除順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [下一個值 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

