---
title: "column_constraint (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/05/2017
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
- column_constraint
- column_constraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
- constraints [SQL Server], properties
- constraints [SQL Server], definitions
- column_constraint
ms.assetid: 8119b7c7-e93b-4de5-8f71-c3b7c70b993c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8530f45f71d231783083b061f1c6e0095770ea53
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-table-columnconstraint-transact-sql"></a>ALTER TABLE column_constraint (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定屬於新的資料行定義，藉由加入至資料表的 PRIMARY KEY、 FOREIGN KEY、 UNIQUE 或 CHECK 條件約束的屬性[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor ]   
        [ WITH ( index_option [, ...n ] ) ]  
        [ ON { partition_scheme_name (partition_column_name)   
            | filegroup | "default" } ]   
    | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name   
            [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>引數  
 CONSTRAINT  
 指定開始定義 PRIMARY KEY、UNIQUE、FOREIGN KEY 或 CHECK 條件約束。  
  
 *constraint_name*  
 這是條件約束的名稱。 條件約束名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)，不同之處在於名稱開頭不能是數字符號 （#）。 如果*constraint_name*是未提供，將系統產生的名稱指派給條件約束。  
  
 NULL | NOT NULL  
 指定資料行是否接受 Null 值。 不允許 NULL 的資料行必須指定了預設值，才能夠加入。 如果新資料行允許 Null 值，且未指定預設值，資料表每個資料列的新資料行都會包含 NULL。 如果新資料行允許 Null 值，且加入了預設定義，就可以利用 WITH VALUE 選項，將預設值儲存在資料表每個現有資料列的新資料行中。  
  
 如果新資料行不允許 Null 值，就必須隨著新資料行加入 DEFAULT 定義。 這個新資料行會在現有資料列的各個新資料行中，自動載入預設值。  
  
 當加入資料行需要實際變更資料表的資料列時，例如，在每個資料列中加入 DEFAULT 值，執行 ALTER TABLE 會保留資料表的鎖定。 這會影響在鎖定就緒時，變更資料表內容的能力。 相對地，加入允許 Null 值且未指定預設值的資料行，只是一項中繼資料作業，不含任何鎖定。  
  
 當您使用 CREATE TABLE 或 ALTER TABLE 時，資料庫和工作階段設定值會影響且可能會覆寫資料行定義所用之資料類型的 Null 屬性。 我們建議您一律將非計算資料行明確定義為 NULL 或 NOT NULL，如果您採用使用者自訂資料類型，建議您允許資料行使用資料類型的預設 Null 屬性。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
 PRIMARY KEY  
 這是一個條件約束，它會利用唯一索引來強制執行一個或多個指定之資料行的實體完整性。 每份資料表都只能建立一個 PRIMARY KEY 條件約束。  
  
 UNIQUE  
 這是一個條件約束，它利用唯一索引來提供一個或多個指定之資料行的實體完整性。  
  
 CLUSTERED | NONCLUSTERED  
 指定建立 PRIMARY KEY 或 UNIQUE 條件約束的叢集或非叢集索引。 PRIMARY KEY 條件約束預設為 CLUSTERED。 UNIQUE 條件約束預設為 NONCLUSTERED。  
  
 如果叢集條件約束或索引已在資料表中，就無法指定 CLUSTERED。 如果叢集條件約束或索引已在資料表中，PRIMARY KEY 條件約束便預設為 NONCLUSTERED。  
  
 資料行**ntext**，**文字**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，或**映像**資料型別不能指定為索引的資料行。  
  
 FILLFACTOR  **=** *填滿因數*  
 指定用來儲存索引資料的每個索引頁面，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 所應加以填滿的程度。 使用者指定的填滿因數值可以是從 1 到 100 之間。 如果未指定值，預設值為 0。  
  
> [!IMPORTANT]  
>  WITH FILLFACTOR =*填滿因數*唯一的索引選項適用於 PRIMARY KEY 或 UNIQUE 條件約束，為了與舊版相容，但將不會記載在這種方式在未來的版本。 可以指定其他索引選項，在[index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md)子句的 ALTER TABLE。  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *檔案群組*  |  **"**預設**"** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定條件約束所建立之索引的儲存位置。 如果*partition_scheme_name*指定，則索引的分割區和資料分割會對應至所指定的檔案群組*partition_scheme_name*。 如果*檔案群組*指定，則會在具名檔案群組中建立索引。 如果**"**預設**"**指定或完全未指定 ON，如果在相同的檔案群組，做為資料表建立索引。 如果加入 PRIMARY KEY 或 UNIQUE 條件約束的叢集索引時指定了 ON，則建立叢集索引時，會將整份資料表移到指定的檔案群組中。  
  
 在這個內容中，default 不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果**"**預設**"**指定，將 QUOTED_IDENTIFIER 選項必須是 ON，目前工作階段。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 FOREIGN KEY REFERENCES  
 這是一個條件約束，它提供資料行中之資料的參考完整性。 FOREIGN KEY 條件約束要求資料行中的每個值存在於所參考之資料表的指定資料行中。  
  
 *schema_name*  
 這是 FOREIGN KEY 條件約束參考之資料表所屬的結構描述名稱。  
  
 *referenced_table_name*  
 這是 FOREIGN KEY 條件約束所參考的資料表。  
  
 *ref_column*  
 這是新 FOREIGN KEY 條件約束所參考的資料行，用括號括住。  
  
 ON DELETE {**採取任何動作**|CASCADE |SET NULL |SET DEFAULT}  
 指定如果變更的資料表中之資料列有參考關聯性，且在父資料表中刪除了所參考的資料列，變更的資料表中之資料列會發生什麼動作。 預設值是 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會產生一則錯誤，且會回復父資料表中之資料列的刪除動作。  
  
 CASCADE  
 如果從父資料表中刪除資料列，便會從進行參考的資料表中刪除對應的資料列。  
  
 SET NULL  
 當刪除父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為 NULL。 若要執行這個條件約束，外部索引鍵資料行必須可為 Null。  
  
 SET DEFAULT  
 當刪除父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為預設值。 若要執行這個條件約束，所有外部索引鍵資料行都必須有預設定義。 如果有可為 Null 的資料行，但沒有設定明確的預設值，NULL 便成為這個資料行的隱含預設值。  
  
 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。 如需邏輯記錄的詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果變更的資料表已有 INSTEAD OF 觸發程序 ON DELETE，便無法定義 ON DELETE CASCADE。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫**ProductVendor**資料表有參考關聯性**廠商**資料表。 **ProductVendor.VendorID**外部索引鍵參考**Vendor.VendorID**主索引鍵。  
  
 如果 DELETE 陳述式會執行中的資料列**廠商**資料表，且 ON DELETE CASCADE 動作指定了**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]會檢查是否有一或多個相依的資料列中**ProductVendor**資料表。 如果任何存在的相依資料列中**ProductVendor**資料表將被刪除，除了中所參考的資料列**廠商**資料表。  
  
 相反地，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引發錯誤，並且會回復 delete 動作上**廠商**資料列中的至少一個資料列時**ProductVendor**在參考的資料表。  
  
 在更新 {**採取任何動作**|CASCADE |SET NULL |SET DEFAULT}  
 指定當變更的資料表中之資料列有參考關聯性，且在父資料表中所參考的資料列有了更新時，變更的資料表中之資料列會發生什麼動作。 預設值是 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生一則錯誤，且會回復父資料表中之資料列的更新動作。  
  
 CASCADE  
 當父資料表中的資料列有了更新時，在進行參考的資料表中，也會更新對應的資料列。  
  
 SET NULL  
 當更新父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為 NULL。 若要執行這個條件約束，外部索引鍵資料行必須可為 Null。  
  
 SET DEFAULT  
 當更新父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為預設值。 若要執行這個條件約束，所有外部索引鍵資料行都必須有預設定義。 如果有可為 Null 的資料行，但沒有設定明確的預設值，NULL 便成為這個資料行的隱含預設值。  
  
 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。 如需邏輯記錄的詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果在 INSTEAD OF 觸發程序 ON UPDATE 已經存在已警示的資料表，則無法定義ON UPDATE CASCADE、SET NULL、或 SET DEFAULT。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫**ProductVendor**資料表有參考關聯性**廠商**資料表。 **ProductVendor.VendorID**外部索引鍵參考**Vendor.VendorID**主索引鍵。  
  
 如果 UPDATE 陳述式會執行中的資料列**廠商**指定資料表和 ON UPDATE CASCADE 動作**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]會檢查是否有一或多個相依的資料列中**ProductVendor**資料表。 如果有的話，相依的資料列中**ProductVendor**資料表將會更新，除了中所參考的資料列**廠商**資料表。  
  
 相反地，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引發錯誤，並且會回復更新動作上**廠商**資料列中的至少一個資料列時**ProductVendor**在參考的資料表。  
  
 NOT FOR REPLICATION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 可以指定給 FOREIGN KEY 條件約束和 CHECK 條件約束。 如果條件約束指定了這個子句，當複寫代理程式執行插入、更新或刪除作業時，不會強制執行這個條件約束。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。  
  
 *logical_expression*  
 CHECK 條件約束所使用的邏輯運算式，會傳回 TRUE 或 FALSE。 *logical_expression*用有檢查條件約束無法參考另一個資料表，但可以參考相同的資料列之相同資料表中的其他資料行。 這個運算式不能參考別名資料類型。  
  
## <a name="remarks"></a>備註  
 加入 FOREIGN KEY 或 CHECK 條件約束時，除非指定 WITH NOCHECK 選項，否則將會驗證所有現有資料的強制違規。 如果有任何違規，ALTER TABLE 便會失敗，且會傳回錯誤。 當現有資料行中加入了新的 PRIMARY KEY 或 UNIQUE 條件約束時，資料行中的資料便必須是唯一的。 如果找到重複的值，ALTER TABLE 便會失敗。 當加入 PRIMARY KEY 或 UNIQUE 條件約束時，WITH NOCHECK 選項沒有作用。  
  
 每個 PRIMARY KEY 和 UNIQUE 條件約束都會產生一個索引。 UNIQUE 和 PRIMARY KEY 條件約束數目無法使資料表的索引數目超出 999 個非叢集索引和 1 個叢集索引。 外部索引鍵條件約束不會自動產生索引。 但外部索引鍵資料行常會用於查詢的聯結準則，方法是將資料表的外部索引鍵條件約束與其他資料表的主要或唯一索引鍵資料行進行比對。 外部索引鍵資料行的索引可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 快速從外部索引鍵資料表中尋找相關資料。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱[ALTER TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)  
  
  
