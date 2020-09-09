---
description: sp_tableoption (Transact-SQL)
title: sp_tableoption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3920007400a4ae407303f3fddff50c0a5ace2328
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534797"
---
# <a name="sp_tableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  設定使用者定義資料表的選項值。 sp_tableoption 可以用來控制具有 **Varchar (max) **、 **Nvarchar (max) **、 **Varbinary (max) **、 **xml**、 **text**、 **Ntext**、 **image**或大型使用者定義型別資料行之資料表的同資料列行為。  
  
> [!IMPORTANT]  
>  未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將移除 text in row 功能。 若要儲存大型值資料，建議您使用 **Varchar (max) **、 **Nvarchar (max) ** 和 **Varbinary (max) ** 資料類型。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>引數  
 [ @TableNamePattern =] '*table*'  
 這是使用者定義資料庫資料表的完整或非完整名稱。 如果提供其中包括資料庫名稱的完整資料表名稱，資料庫名稱就必須是目前資料庫的名稱。 您不能同時設定多份資料表的資料表選項。 *資料表* 是 **Nvarchar (776) **，沒有預設值。  
  
 [ @OptionName =] '*option_name*'  
 這是資料表選項名稱。 *option_name* 是 **Varchar (35) **，沒有預設值 Null。 *option_name* 可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|table lock on bulk load|當停用 (預設值) 時，它會讓使用者定義資料表上的大量載入程序取得資料列鎖定。 當啟用時，使用者定義資料表的大量載入處理序會取得大量更新鎖定。|  
|insert row lock|不再支援。<br /><br /> 這個選項對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的鎖定行為沒有影響，併入它的目的，只是為了與現有的指令碼和程序相容。|  
|text in row|當它是 OFF 或 0 (停用，預設值) 時，它不會變更目前的行為，資料列中沒有 BLOB。<br /><br /> 當指定且 @OptionValue 為 ON (enabled) 或24到7000的整數值時，新的 **text**、 **Ntext**或 **image** 字串會直接儲存在資料列中。 當更新 BLOB 值時，所有現有的 BLOB (二進位大型物件： **text**、 **Ntext**或 **image** 資料) 都會變更為 text in row 格式。 如需詳細資訊，請參閱＜備註＞。|  
|large value types out of row|1 = **Varchar (max) **、 **Nvarchar (max) **、 **Varbinary (max) **、 **xml** 和大型使用者定義型別 (UDT) 資料表中的資料行會儲存在資料列外，並以16位元組指標指向根。<br /><br /> 0 = **Varchar (max) **、 **Nvarchar (max) **、 **Varbinary (max) **、 **xml** 和大型 UDT 值直接儲存在資料列中，最多可達8000個位元組的限制，而且只要該值可以容納在記錄中即可。 如果記錄無法容納值，便會將指標儲存在同資料列中，其餘部分會儲存在資料列外 (LOB 儲存空間中)。 預設值是 0。<br /><br />  (UDT) 的大型使用者定義型別適用于： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。 <br /><br /> 使用 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 的 TEXTIMAGE_ON 選項，即可指定大型資料類型的儲存位置。 |  
|Vardecimal 儲存格式|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本。<br /><br /> 若為 TRUE、ON 或 1，指定的資料表會啟用為 Vardecimal 儲存格式。 若為 FALSE、OFF 或 0，資料表則不會啟用為 Vardecimal 儲存格式。 只有當資料庫已使用 [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)啟用 vardecimal 儲存格式時，才能啟用 vardecimal 儲存格式。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中， **vardecimal** 儲存格式已被取代。 請改用資料列壓縮。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。 預設值是 0。|  
  
 [ @OptionValue =] '*value*'  
 這是指 *option_name* 是啟用 (TRUE、ON 或 1) 或停用 (FALSE、OFF 或 0) 。 *值* 是 **Varchar (12) **，沒有預設值。 *值* 不區分大小寫。  
  
 text in row 選項的有效選項值是 0、ON、OFF，或 24 至 7000 的整數。 當 *值* 為 ON 時，限制會預設為256個位元組。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或錯誤號碼 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_tableoption 只能用來設定使用者定義資料表的選項值。 若要顯示資料表屬性，請使用 OBJECTPROPERTY 或查詢 sys. 資料表。  
  
 只有包含文字資料行的資料表能夠啟用或停用 sp_tableoption 中的 text in row 選項。 如果資料表沒有文字資料行，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會產生錯誤。  
  
 當啟用 text in row 選項時，此 @OptionValue 參數可讓使用者指定要儲存在 BLOB 的資料列中的大小上限。 預設值是 256 個位元組，但值的範圍在 24 和 7000 個位元組之間。  
  
 如果符合下列條件，則會將**text**、 **Ntext**或**image**字串儲存在資料列中：  
  
-   啟用 text in row。  
  
-   字串的長度比指定的限制短 @OptionValue  
  
-   資料列包含足夠的空間。  
  
 當 BLOB 字串儲存在資料列中時，讀取和寫入 **text**、 **Ntext**或 **image** 字串的速度可以像讀取或寫入字元和二進位字串一樣快。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不必存取個別頁面，即可讀取或寫入 BLOB 字串。  
  
 如果 **text**、 **Ntext**或 **image** 字串大於指定的限制或資料列中的可用空間，則會改為將指標儲存在資料列中。 將 BLOB 字串儲存在資料列的條件仍適用，不過，資料列必須有足以保留指標的空間。  
  
 儲存在資料表資料列中之 BLOB 字串和指標的處理方式，類似於可變長度的字串。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會使用儲存字串或指標所需要的位元組數。  
  
 當第一次啟用 text in row 時，不會立即轉換現有的 BLOB 字串。 只有在更新字串時，才會轉換字串。 同樣地，當 text in row 選項限制增加時，在資料列 **中的 text、** **Ntext**或 **image** 字串將不會轉換成符合新的限制，直到更新為止。  
  
> [!NOTE]  
>  停用 text in row 選項或縮減選項限制，必須轉換所有 BLOB；因此，隨著必須轉換的 BLOB 字串數目而不同，程序可能會很長。 在轉換程序中，會鎖定這份資料表。  
  
 資料表變數 (包括傳回資料表變數的函數) 會自動擁有啟用了預設內嵌限制 256 的 text in row 選項。 這個選項無法變更。  
  
 text in row 選項支援 TEXTPTR、WRITETEXT、UPDATETEXT 和 READTEXT 函數。 使用者可以利用 SUBSTRING() 函數來讀取 BLOB 的各部分，但必須記住同資料列文字指標的持續時間和數目限制與其他文字指標不同。  
  
 若要將資料表從 Vardecimal 儲存格式變更回一般的十進位儲存格式，資料庫必須處於 SIMPLE 復原模式。 變更復原模式會中斷備份所需的記錄鏈結，因此，請先建立完整的資料庫備份，再從資料表移除 Vardecimal 儲存格式。  
  
 如果您要將現有的 LOB 資料類型資料行轉換 (text、Ntext 或 image) 為小型到中型的大型實值型別 (Varchar (max) 、Nvarchar (max) 或 Varbinary (max) max large_value_types_out_of_row # A9，大部分的語句都不會參考您環境中的大數數值型別資料行，請考慮將**large_value_types_out_of_row**變更為**1**以獲得最佳效能。 當 **large_value_types_out_of_row** 選項值變更時，現有的 Varchar (max) 、Nvarchar (max) 、Varbinary (max) 和 xml 值都不會立即轉換。 字串的儲存會在後續更新時會變更。 任何插入資料表的新值會根據生效的資料表選項來儲存。 為了立即得到結果，請建立資料的複本，然後在變更 **large_value_types_out_of_row** 設定或將每個小到中大數數值型別資料行更新為本身，以便變更字串的儲存，並使資料表選項生效。 更新或重新擴展以緊縮資料表之後，請重新建立資料表的索引。 
    
  
## <a name="permissions"></a>權限  
 執行 sp_tableoption 需要資料表的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. 儲存資料列外的 xml 資料  
 下列範例會指定將資料表中的 **xml** 資料 `HumanResources.JobCandidate` 儲存在資料列之外。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. 在資料表上啟用 Vardecimal 儲存格式  
 下列範例會修改 `Production.WorkOrderRouting` 資料表，以儲存 `decimal` 資料類型的單元 `vardecimal` 格式。  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
