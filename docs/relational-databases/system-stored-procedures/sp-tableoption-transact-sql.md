---
title: "sp_tableoption (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b468d62444bd3c9217cc7f931a2786034baec12
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sptableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  設定使用者定義資料表的選項值。 sp_tableoption 可以用來控制資料表的 in-row 行為**varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，**文字**， **ntext**，**映像**，或大型使用者定義型別資料行。  
  
> [!IMPORTANT]  
>  未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將移除 text in row 功能。 若要儲存大數值資料，我們建議您使用的**varchar （max)**， **nvarchar （max)**和**varbinary （max)**資料型別。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>引數  
 [ @TableNamePattern =] '*資料表*'  
 這是使用者定義資料庫資料表的完整或非完整名稱。 如果提供其中包括資料庫名稱的完整資料表名稱，資料庫名稱就必須是目前資料庫的名稱。 您不能同時設定多份資料表的資料表選項。 *資料表*是**nvarchar(776)**，沒有預設值。  
  
 [ @OptionName =] '*option_name*'  
 這是資料表選項名稱。 *option_name*是**varchar （35)**，沒有預設值是 NULL。 *option_name*可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|table lock on bulk load|當停用 (預設值) 時，它會讓使用者定義資料表上的大量載入程序取得資料列鎖定。 當啟用時，使用者定義資料表的大量載入處理序會取得大量更新鎖定。|  
|insert row lock|不再支援。<br /><br /> 這個選項對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的鎖定行為沒有影響，併入它的目的，只是為了與現有的指令碼和程序相容。|  
|text in row|當它是 OFF 或 0 (停用，預設值) 時，它不會變更目前的行為，資料列中沒有 BLOB。<br /><br /> 當指定和@OptionValue是 ON （已啟用） 或 24 至 7000 之間，新的整數值**文字**， **ntext**，或**映像**字串會直接儲存在資料列。 所有現有的 BLOB (二進位大型物件：**文字**， **ntext**，或**映像**資料) 將會更新 BLOB 值時變更為 text in row 格式。 如需詳細資訊，請參閱＜備註＞。|  
|large value types out of row|1 = **varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**並儲存在資料表中的大型使用者定義型別 (UDT) 資料行資料列外部，並且以 16 位元組指標指向根。<br /><br /> 0 = **varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**和大型 UDT 值直接儲存在資料列時，最大限制8000 個位元組，只要可以容納在記錄中的值。 如果記錄無法容納值，便會將指標儲存在同資料列中，其餘部分會儲存在資料列外 (LOB 儲存空間中)。 預設值為 0。<br /><br /> 大型使用者定義型別 (UDT) 適用於：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 <br /><br /> 使用 TEXTIMAGE_ON 選項[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)指定大型資料類型的儲存體的位置。 |  
|Vardecimal 儲存格式|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 若為 TRUE、ON 或 1，指定的資料表會啟用為 Vardecimal 儲存格式。 若為 FALSE、OFF 或 0，資料表則不會啟用為 Vardecimal 儲存格式。 只有在使用資料庫啟用為 vardecimal 儲存格式時，就可以啟用 Vardecimal 儲存格式[sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)。 在[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和更新版本， **vardecimal**儲存格式已被取代。 請改用資料列壓縮。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。 預設值為 0。|  
  
 [ @OptionValue =] '*值*'  
 為是否*option_name*已啟用 （TRUE、 ON 或 1） 或停用 (FALSE、 OFF 或 0)。 *值*是**varchar(12)**，沒有預設值。 *值*是不區分大小寫。  
  
 text in row 選項的有效選項值是 0、ON、OFF，或 24 至 7000 的整數。 當*值*是 ON 時，限制會預設為 256 個位元組。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或錯誤號碼 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_tableoption 只能用來設定使用者定義資料表的選項值。 若要顯示資料表屬性，請使用 OBJECTPROPERTY。  
  
 只有包含文字資料行的資料表能夠啟用或停用 sp_tableoption 中的 text in row 選項。 如果資料表沒有文字資料行，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會產生錯誤。  
  
 當啟用 text in row 選項時，@OptionValue參數可讓使用者指定的資料列中儲存 blob 的大小上限。 預設值是 256 個位元組，但值的範圍在 24 和 7000 個位元組之間。  
  
 **文字**， **ntext**，或**映像**字串會儲存在資料列，如果符合下列條件：  
  
-   啟用 text in row。  
  
-   字串的長度小於指定的限制@OptionValue  
  
-   資料列包含足夠的空間。  
  
 當 BLOB 字串儲存在資料列時，讀取和寫入**文字**， **ntext**，或**映像**字串可以跟讀取或寫入字元和二進位字串一樣快。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不必存取個別頁面，即可讀取或寫入 BLOB 字串。  
  
 如果**文字**， **ntext**，或**映像**字串大於指定的限制或資料列中的可用空間，指標會改為儲存在資料列。 將 BLOB 字串儲存在資料列的條件仍適用，不過，資料列必須有足以保留指標的空間。  
  
 儲存在資料表資料列中之 BLOB 字串和指標的處理方式，類似於可變長度的字串。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會使用儲存字串或指標所需要的位元組數。  
  
 當第一次啟用 text in row 時，不會立即轉換現有的 BLOB 字串。 只有在更新字串時，才會轉換字串。 同樣地，text in row 選項限制會增加，**文字**， **ntext**，或**映像**不會轉換已在資料列中的字串來遵照新的限制之前更新它們的時間。  
  
> [!NOTE]  
>  停用 text in row 選項或縮減選項限制，必須轉換所有 BLOB；因此，隨著必須轉換的 BLOB 字串數目而不同，程序可能會很長。 在轉換程序中，會鎖定這份資料表。  
  
 資料表變數 (包括傳回資料表變數的函數) 會自動擁有啟用了預設內嵌限制 256 的 text in row 選項。 這個選項無法變更。  
  
 Text in row 選項支援 TEXTPTR、 WRITETEXT、 UPDATETEXT 和 READTEXT 函數。 使用者可以利用 SUBSTRING() 函數來讀取 BLOB 的各部分，但必須記住同資料列文字指標的持續時間和數目限制與其他文字指標不同。  
  
 若要將資料表從 Vardecimal 儲存格式變更回一般的十進位儲存格式，資料庫必須處於 SIMPLE 復原模式。 變更復原模式會中斷備份所需的記錄鏈結，因此，請先建立完整的資料庫備份，再從資料表移除 Vardecimal 儲存格式。  
  
 如果您要將現有 LOB 資料類型資料行 （text、 ntext 或 image） 轉換成小型至中型大數值類型 （varchar （max）、 nvarchar （max），或 varbinary，以及大部分陳述式執行不參考您的環境中的大數值類型資料行，請考慮變更**large_value_types_out_of_row**至**1**取得最佳效能。 當**large_value_types_out_of_row**選項值已變更，現有的 varchar （max）、 nvarchar （max）、 varbinary （max），以及 xml 值不會立即轉換。 字串的儲存會在後續更新時會變更。 任何插入資料表的新值會根據生效的資料表選項來儲存。 立即的結果，請建立一份資料，然後再變更之後重新擴展資料表**large_value_types_out_of_row**設定或更新至其本身的每個小型至中型大數值類型資料行，讓的儲存體字串是作用中變更資料表選項。 更新或重新擴展以緊縮資料表之後，請重新建立資料表的索引。 
    
  
## <a name="permissions"></a>Permissions  
 執行 sp_tableoption 需要資料表的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. 儲存資料列外的 xml 資料  
 下列範例會指定**xml**中的資料`HumanResources.JobCandidate`資料表資料列外儲存。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. 在資料表上啟用 Vardecimal 儲存格式  
 下列範例會修改`Production.WorkOrderRouting`可儲存資料表`decimal`中的資料類型`vardecimal`儲存格式。  

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
  
## <a name="see-also"></a>請參閱＜  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Database Engine 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
