---
title: "table_constraint (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f5265366f28f302e69a178f45baa4464efa1bfd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-tableconstraint-transact-sql"></a>ALTER TABLE table_constraint (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定的主索引鍵、 UNIQUE、 FOREIGN KEY、 CHECK 條件約束或 DEFAULT 定義加入至資料表使用屬性[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>引數  
 CONSTRAINT  
 指定開始定義 PRIMARY KEY、UNIQUE、FOREIGN KEY 或 CHECK 條件約束，或 DEFAULT。  
  
 *constraint_name*  
 這是條件約束的名稱。 條件約束名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)，不同之處在於名稱開頭不能是數字符號 （#）。 如果未提供 constraint_name，就會將系統產生的名稱指派給條件約束。  
  
 PRIMARY KEY  
 這是一個條件約束，它會利用唯一索引來強制執行一個或多個指定之資料行的實體完整性。 每份資料表都只能建立一個 PRIMARY KEY 條件約束。  
  
 UNIQUE  
 這是一個條件約束，它利用唯一索引來提供一個或多個指定之資料行的實體完整性。  
  
 CLUSTERED | NONCLUSTERED  
 指定建立 PRIMARY KEY 或 UNIQUE 條件約束的叢集或非叢集索引。 PRIMARY KEY 條件約束預設為 CLUSTERED。 UNIQUE 條件約束預設為 NONCLUSTERED。  
  
 如果叢集條件約束或索引已在資料表中，就無法指定 CLUSTERED。 如果叢集條件約束或索引已在資料表中，PRIMARY KEY 條件約束便預設為 NONCLUSTERED。  
  
 資料行**ntext**，**文字**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，或**映像**資料型別不能指定為索引的資料行。  
  
 *資料行*  
 這是新條件約束中所用的一個資料行或一份資料行清單 (用括號括住來指定)。  
  
 [ **ASC** |DESC]  
 指定一個或多個資料行參與資料表條件約束的排序順序。 預設值是 ASC。  
  
 FILLFACTOR  **=** *填滿因數*  
 指定用來儲存索引資料的每個索引頁面，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 所應加以填滿的程度。 使用者指定*填滿因數*值可以是從 1 到 100 之間。 如果未指定值，預設值為 0。  
  
> [!IMPORTANT]  
>  WITH FILLFACTOR =*填滿因數*唯一的索引選項適用於 PRIMARY KEY 或 UNIQUE 條件約束，為了與舊版相容，但將不會記載在這種方式在未來的版本。 可以指定其他索引選項，在[index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md)子句的 ALTER TABLE。  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *檔案群組* |  **"**預設**"** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定條件約束所建立之索引的儲存位置。 如果*partition_scheme_name*指定，則索引的分割區和資料分割會對應至所指定的檔案群組*partition_scheme_name*。 如果*檔案群組*指定，則會在具名檔案群組中建立索引。 如果**"**預設**"**指定或完全未指定 ON，如果在相同的檔案群組，做為資料表建立索引。 如果加入 PRIMARY KEY 或 UNIQUE 條件約束的叢集索引時指定了 ON，則建立叢集索引時，會將整份資料表移到指定的檔案群組中。  
  
 在此內容中，預設值不是關鍵字;它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果**"**預設**"**指定，將 QUOTED_IDENTIFIER 選項必須是 ON，目前工作階段。 這是預設值。  
  
 FOREIGN KEY REFERENCES  
 這是一個條件約束，它提供資料行中之資料的參考完整性。 FOREIGN KEY 條件約束要求資料行中的每個值存在於所參考之資料表的指定資料行中。  
  
 *referenced_table_name*  
 這是 FOREIGN KEY 條件約束所參考的資料表。  
  
 *ref_column*  
 這是新 FOREIGN KEY 條件約束所參考的一個資料行或一份資料行清單 (用括號括住)。  
  
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
  
 如果 DELETE 陳述式會執行中的資料列**廠商**資料表且 ON DELETE CASCADE 動作指定了**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]會檢查是否有一或多個相依的資料列中**ProductVendor**資料表。 如果任何存在的相依資料列中**ProductVendor**資料表將被刪除，除了中所參考的資料列**廠商**資料表。  
  
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
  
 如果 UPDATE 陳述式會執行中的資料列**廠商**指定資料表和 ON UPDATE CASCADE 動作**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]會檢查是否有一或多個相依的資料列中**ProductVendor**資料表。 如果有的話，相依的資料列中**ProductVendor**資料表將會更新，以及中所參考的資料列**廠商**資料表。  
  
 相反地，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引發錯誤，並且會回復更新動作上**廠商**資料列中的至少一個資料列時**ProductVendor**在參考的資料表。  
  
 NOT FOR REPLICATION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 可以指定給 FOREIGN KEY 條件約束和 CHECK 條件約束。 如果條件約束指定了這個子句，當複寫代理程式執行插入、更新或刪除作業時，不會強制執行這個條件約束。  
  
 DEFAULT  
 指定資料行的預設值。 您可以利用 DEFAULT 定義來提供現有資料列之新資料行的值。 無法將具有資料行加入 DEFAULT 定義**時間戳記**資料類型、 IDENTITY 屬性，現有的 DEFAULT 定義或繫結預設值。 如果資料行有現有的預設值，就必須先卸除預設值，才能加入新預設值。 如果使用者定義型別資料行指定預設值，類型應該支援的隱含轉換*constant_expression*使用者定義型別。 若要維護與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性，您可以將條件約束名稱指派給 DEFAULT。  
  
 *constant_expression*  
 這是用來作為資料行預設值的常值、NULL 或系統函數。 如果*constant_expression*在搭配使用具有資料行定義為屬於[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]使用者定義型別之型別的實作必須支援的隱含轉換*constant_運算式*使用者定義型別。  
  
 如*資料行*  
 指定關聯於資料表層級 DEFAULT 定義的資料行。  
  
 WITH VALUES  
 在預設提供的值會指定*constant_expression*會儲存在新的資料行加入至現有的資料列。 只有在 ADD 資料行子句指定了 DEFAULT 時，才能指定 WITH VALUES。 如果加入的資料行允許 Null 值，且指定了 WITH VALUES，就會將預設值儲存在加入現有資料列的新資料行中。 如果允許 NULL 的資料行沒有指定 WITH VALUES，就會將 NULL 儲存在現有資料列的新資料行中。 如果新資料行不允許 NULL，就會將預設值儲存在新資料列中，不論是否指定了 WITH VALUES，都是如此。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。  
  
 *logical_expression*  
 CHECK 條件約束所使用的邏輯運算式，會傳回 TRUE 或 FALSE。 *logical_expression*用有檢查條件約束無法參考另一個資料表，但可以參考相同的資料列之相同資料表中的其他資料行。 這個運算式不能參考別名資料類型。  
  
## <a name="remarks"></a>備註  
 加入 FOREIGN KEY 或 CHECK 條件約束時，除非指定 WITH NOCHECK 選項，否則將會驗證所有現有資料的強制違規。 如果有任何違規，ALTER TABLE 便會失敗，且會傳回錯誤。 當現有資料行中加入了新的 PRIMARY KEY 或 UNIQUE 條件約束時，資料行中的資料便必須是唯一的。 如果找到重複的值，ALTER TABLE 便會失敗。 當加入 PRIMARY KEY 或 UNIQUE 條件約束時，WITH NOCHECK 選項沒有作用。  
  
 每個 PRIMARY KEY 和 UNIQUE 條件約束都會產生一個索引。 UNIQUE 和 PRIMARY KEY 條件約束數目無法使資料表的索引數目超出 999 個非叢集索引和 1 個叢集索引。 外部索引鍵條件約束不會自動產生索引。 但外部索引鍵資料行常會用於查詢的聯結準則，方法是將資料表的外部索引鍵條件約束與其他資料表的主要或唯一索引鍵資料行進行比對。 外部索引鍵資料行的索引可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 快速從外部索引鍵資料表中尋找相關資料。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱[ALTER TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

