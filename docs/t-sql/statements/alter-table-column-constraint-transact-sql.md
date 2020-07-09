---
title: column_constraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a54784e777f85fea73036df3f0c6ec0b23be878e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760986"
---
# <a name="alter-table-column_constraint-transact-sql"></a>ALTER TABLE column_constraint (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  指定 PRIMARY KEY、FOREIGN KEY、UNIQUE 或 CHECK 條件約束的屬性，而這些條件約束是使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 新增至資料表之新資料行定義的一部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
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
 這是條件約束的名稱。 條件約束名稱必須遵照[識別碼](../../relational-databases/databases/database-identifiers.md)的規則，不過，名稱開頭不能是數字符號 (#)。 如果未提供 *constraint_name*，就會將系統產生的名稱指派給條件約束。  
  
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
  
 屬於 **ntext**、**text**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml** 或 **image** 資料類型的資料行無法指定為索引的資料行。  
  
 WITH FILLFACTOR **=** _fillfactor_  
 指定用來儲存索引資料的每個索引頁面，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 所應加以填滿的程度。 使用者指定的填滿因數可以是從 1 到 100 的值。 如果未指定值，預設值為 0。  
  
> [!IMPORTANT]  
>  為了與舊版相容，我們保持將 WITH FILLFACTOR = *fillfactor* 記載為適用於 PRIMARY KEY 或 UNIQUE 條件約束的唯一索引選項，但未來版本的文件不會再依照這個方式來說明。 您可以在 ALTER TABLE 的 [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) 子句中，指定其他索引選項。  
  
 ON { _partition_scheme_name_ **(** _partition_column_name_ **)**  | *filegroup* |  **"** default **"** } **適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本。  
  
 指定條件約束所建立之索引的儲存位置。 如果指定 *partition_scheme_name*，索引就會進行資料分割，這些資料分割會對應於 *partition_scheme_name* 所指定的檔案群組。 如果指定了 *filegroup*，就會在具名檔案群組中建立索引。 如果指定了 **"** default **"** ，或完全未指定 ON，就會在與資料表相同的檔案群組中建立索引。 如果加入 PRIMARY KEY 或 UNIQUE 條件約束的叢集索引時指定了 ON，則建立叢集索引時，會將整份資料表移到指定的檔案群組中。  
  
 在這個內容中，default 不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"** default **"** 或 ON **[** default **]** 。 如果指定了 **"** default **"** ，則目前工作階段的 QUOTED_IDENTIFIER 選項就必須是 ON。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 FOREIGN KEY REFERENCES  
 這是一個條件約束，它提供資料行中之資料的參考完整性。 FOREIGN KEY 條件約束要求資料行中的每個值存在於所參考之資料表的指定資料行中。  
  
 *schema_name*  
 這是 FOREIGN KEY 條件約束參考之資料表所屬的結構描述名稱。  
  
 *referenced_table_name*  
 這是 FOREIGN KEY 條件約束所參考的資料表。  
  
 *ref_column*  
 這是新 FOREIGN KEY 條件約束所參考的資料行，用括號括住。  
  
 ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
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
  
 例如在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中，**ProductVendor** 資料表與 **Vendor** 資料表有參考關聯性。 **ProductVendor.VendorID** 外部索引鍵會參考 **Vendor.VendorID** 主索引鍵。  
  
 如果在 **Vendor** 資料表的某資料列上執行 DELETE 陳述式，且指定了 **ProductVendor.VendorID** 的 ON DELETE CASCADE 動作，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 便會檢查 **ProductVendor** 資料表中一或多個相依的資料列。 如果有任何相依的資料列存在，除了會將 **Vendor** 資料表中所參考的資料列刪除，還會刪除 **ProductVendor** 資料表中的相依資料列。  
  
 相反地，如果指定 NO ACTION，當 [!INCLUDE[ssDE](../../includes/ssde-md.md)]ProductVendor**資料表中有至少一個資料列參考**Vendor **資料列時，** 會產生一則錯誤，且會回復 Vendor 資料列的刪除動作。  
  
 ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
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
  
 例如在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中，**ProductVendor** 資料表與 **Vendor** 資料表有參考關聯性。 **ProductVendor.VendorID** 外部索引鍵會參考 **Vendor.VendorID** 主索引鍵。  
  
 如果在 **Vendor** 資料表的某資料列上執行 UPDATE 陳述式，且指定了 **ProductVendor.VendorID** 的 ON UPDATE CASCADE 動作，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 便會檢查 **ProductVendor** 資料表中一或多個相依的資料列。 如果有任何相依的資料列存在，除了 **Vendor** 資料表中所參考的資料列，還會更新 **ProductVendor** 資料表中的相依資料列。  
  
 相反地，如果指定了 NO ACTION，當 [!INCLUDE[ssDE](../../includes/ssde-md.md)]ProductVendor **資料表中有至少一個資料列參考 Vendor 資料列時，** 會產生一則錯誤，且會回復 **Vendor** 資料列的更新動作。  
  
 NOT FOR REPLICATION  
 **適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本。  
  
 可以指定給 FOREIGN KEY 條件約束和 CHECK 條件約束。 如果條件約束指定了這個子句，當複寫代理程式執行插入、更新或刪除作業時，不會強制執行這個條件約束。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。  
  
 *logical_expression*  
 CHECK 條件約束所使用的邏輯運算式，會傳回 TRUE 或 FALSE。 搭配 CHECK 條件約束使用的 *logical_expression* 無法參考其他資料表，但可以參考相同資料列所在之資料表的其他資料行。 這個運算式不能參考別名資料類型。  
  
## <a name="remarks"></a>備註  
 加入 FOREIGN KEY 或 CHECK 條件約束時，除非指定 WITH NOCHECK 選項，否則將會驗證所有現有資料的強制違規。 如果有任何違規，ALTER TABLE 便會失敗，且會傳回錯誤。 當現有資料行中加入了新的 PRIMARY KEY 或 UNIQUE 條件約束時，資料行中的資料便必須是唯一的。 如果找到重複的值，ALTER TABLE 便會失敗。 當加入 PRIMARY KEY 或 UNIQUE 條件約束時，WITH NOCHECK 選項沒有作用。  
  
 每個 PRIMARY KEY 和 UNIQUE 條件約束都會產生一個索引。 UNIQUE 和 PRIMARY KEY 條件約束數目無法使資料表的索引數目超出 999 個非叢集索引和 1 個叢集索引。 外部索引鍵條件約束不會自動產生索引。 但外部索引鍵資料行常會用於查詢的聯結準則，方法是將資料表的外部索引鍵條件約束與其他資料表的主要或唯一索引鍵資料行進行比對。 外部索引鍵資料行的索引可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 快速從外部索引鍵資料表中尋找相關資料。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)  
  
  
