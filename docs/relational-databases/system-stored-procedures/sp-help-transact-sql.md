---
title: sp_help （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac6e69db443bd23c3e9b1119b21d8fd98ebe39c4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815515"
---
# <a name="sp_help-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  報告資料庫物件（ **sysobjects**相容性檢視中所列的任何物件）、使用者定義資料類型或資料類型的相關資訊。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @objname = ] 'name'`這是任何物件的名稱， **sysobjects**或**systypes**資料表中的任何使用者自訂資料類型。 *name*是**Nvarchar （** 776 **）**，預設值是 Null。 不接受資料庫名稱。  兩個或三個部分的名稱必須加以分隔，例如 'Person.AddressType' 或 [Person.AddressType]。   
   
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回的結果集會根據*名稱*是否已指定、指定時間，以及它是哪個資料庫物件而定。  
  
1.  如果執行**sp_help**不含任何引數，則會傳回目前資料庫中所有類型之物件的摘要資訊。  
  
    |資料行名稱|資料類型|描述|  
    |-----------------|---------------|-----------------|  
    |**名稱**|**Nvarchar （** 128 **）**|物件名稱|  
    |**擁有者**|**Nvarchar （** 128 **）**|物件擁有者 (這是擁有物件的資料庫主體， 預設為包含物件之結構描述的擁有者)。|  
    |**Object_type**|**Nvarchar （** 31 **）**|物件類型|  
  
2.  如果*name*是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型或使用者自訂資料類型， **sp_help**會傳回這個結果集。  
  
    |資料行名稱|資料類型|描述|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**Nvarchar （** 128 **）**|資料類型名稱。|  
    |**Storage_type**|**Nvarchar （** 128 **）**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型名稱。|  
    |**長度**|**smallint**|資料類型的實際長度 (以位元組為單位)。|  
    |**Prec**|**int**|有效位數 (總位數)。|  
    |**縮放比例**|**int**|小數點右側的位數。|  
    |**可為 Null**|**Varchar （** 35 **）**|指出是否允許 NULL 值：[是] 或 [否]。|  
    |**Default_name**|**Nvarchar （** 128 **）**|與這個類型繫結的預設值名稱。<br /><br /> NULL = 未繫結預設值。|  
    |**Rule_name**|**Nvarchar （** 128 **）**|與這個類型繫結的規則名稱。<br /><br /> NULL = 未繫結預設值。|  
    |**定序**|**sysname**|資料類型的定序。 非字元資料類型是 NULL。|  
  
3.  如果*name*是資料類型以外的任何資料庫物件， **sp_help**會根據指定的物件類型，傳回此結果集和其他結果集。  

    |資料行名稱|資料類型|描述|  
    |-----------------|---------------|-----------------|  
    |**名稱**|**Nvarchar （** 128 **）**|資料表名稱|  
    |**擁有者**|**Nvarchar （** 128 **）**|資料表擁有者|  
    |**類型**|**Nvarchar （** 31 **）**|資料表類型|  
    |**Created_datetime**|**datetime**|資料表的建立日期|  
  
     視指定的資料庫物件而定， **sp_help**會傳回額外的結果集。  
  
     如果*name*是系統資料表、使用者資料表或 view， **sp_help**會傳回下列結果集。 不過，不會傳回描述資料檔在檔案群組中之位置的結果集。  
  
    -   在資料行物件上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**Nvarchar （** 128 **）**|資料行名稱。|  
        |**類型**|**Nvarchar （** 128 **）**|資料行資料類型。|  
        |**過**|**Varchar （** 35 **）**|指出是否計算資料行中的值：[是] 或 [否]。|  
        |**長度**|**int**|資料行長度 (以位元組為單位)。<br /><br /> 注意：如果資料類型是大數數值型別（**Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （max）** 或**xml**），此值會顯示為-1。|  
        |**Prec**|**char （** 5 **）**|資料行有效位數。|  
        |**縮放比例**|**char （** 5 **）**|資料行小數位數。|  
        |**可為 Null**|**Varchar （** 35 **）**|指出資料行是否允許 NULL 值：[是] 或 [否]。|  
        |**TrimTrailingBlanks**|**Varchar （** 35 **）**|修剪尾端空白。 傳回 [是] 或 [否]。|  
        |**FixedLenNullInSource**|**Varchar （** 35 **）**|只是為了與舊版相容。|  
        |**定序**|**sysname**|資料行的定序。 非字元資料類型是 NULL。|  
  
    -   在識別欄位上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**身分識別**|**Nvarchar （** 128 **）**|資料類型宣告為識別的資料行名稱。|  
        |**Seed**|**numeric**|識別欄位的起始值。|  
        |**連續**|**numeric**|這個資料行的值所用的遞增。|  
        |**Not For Replication**|**int**|當複寫登入（例如**sqlrepl**）將資料插入資料表時，不會強制執行 IDENTITY 屬性：<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   在資料行上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|全域唯一識別碼資料行的名稱。|  
  
    -   在檔案群組上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**Nvarchar （** 128 **）**|資料所在的檔案群組：「主要」、「次要」或「交易記錄」。|  
  
    -   在索引上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|索引名稱。|  
        |**Index_description**|**Varchar （** 210 **）**|索引的描述。|  
        |**index_keys**|**Nvarchar （** 2078 **）**|建立索引的資料行名稱。 如果是 xVelocity 記憶體最佳化的資料行存放區索引，則傳回 NULL。|  
  
    -   在條件約束上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**Nvarchar （** 146 **）**|條件約束的類型。|  
        |**constraint_name**|**Nvarchar （** 128 **）**|條件約束的名稱。|  
        |**delete_action**|**Nvarchar （** 9 **）**|指出 DELETE 動作是：NO_ACTION、CASCADE、SET_NULL、SET_DEFAULT 或 N/A。<br /><br /> 只適用於 FOREIGN KEY 條件約束。|  
        |**update_action**|**Nvarchar （** 9 **）**|指出 UPDATE 動作是：NO_ACTION、CASCADE、SET_NULL、SET_DEFAULT 或 N/A。<br /><br /> 只適用於 FOREIGN KEY 條件約束。|  
        |**status_enabled**|**Varchar （** 8 **）**|指出是否啟用條件約束：已啟用、已停用或 N/A。<br /><br /> 只適用於 CHECK 和 FOREIGN KEY 條件約束。|  
        |**status_for_replication**|**Varchar （** 19 **）**|指出條件約束是否針對複寫。<br /><br /> 只適用於 CHECK 和 FOREIGN KEY 條件約束。|  
        |**constraint_keys**|**Nvarchar （** 2078 **）**|組成條件約束的資料行名稱，如果是預設值和規則，便是定義預設值或規則的文字。|  
  
    -   在進行參考的物件上傳回的其他結果集：  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**資料表的參考者**|**Nvarchar （** 516 **）**|識別參考資料表的其他資料庫物件。|  
  
    -   在預存程序、函數或擴充預存程序上傳回的其他結果集。  
  
        |資料行名稱|資料類型|描述|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**Nvarchar （** 128 **）**|預存程序參數名稱。|  
        |**類型**|**Nvarchar （** 128 **）**|預存程序參數的資料類型。|  
        |**長度**|**smallint**|最大的實體儲存體長度 (以位元組為單位)。|  
        |**Prec**|**int**|有效位數或總位數。|  
        |**縮放比例**|**int**|小數點右側的位數。|  
        |**Param_order**|**smallint**|參數的順序。|  
  
## <a name="remarks"></a>備註  
 **Sp_help**程式只會在目前資料庫中尋找物件。  
  
 如果未指定*name* ， **sp_help**會列出目前資料庫中所有物件的物件名稱、擁有者和物件類型。 **sp_helptrigger**提供觸發程式的相關資訊。  
  
 **sp_help**只會公開能排序的索引資料行;因此，它不會公開 XML 索引或空間索引的相關資訊。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。 使用者在*objname*上必須至少有一個許可權。 若要檢視資料行條件約束索引鍵、預設值或規則，您必須具有此資料表的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-information-about-all-objects"></a>A. 傳回所有物件的相關資訊  
 下列範例會列出 `master` 資料庫中每個物件的相關資訊。  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. 傳回單一物件的相關資訊  
 下列範例會顯示 `Person` 資料表的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sysobjects &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
