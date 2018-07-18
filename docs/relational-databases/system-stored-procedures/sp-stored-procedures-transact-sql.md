---
title: sp_stored_procedures (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e4f11ee53e27ba983098d20e6b40ee0c0ef176d7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261987"
---
# <a name="spstoredprocedures-transact-sql"></a>sp_stored_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前環境中的預存程序清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@sp_name =** ] **'***name***'**  
 這是用來傳回目錄資訊的程序名稱。 *名稱*是**nvarchar(390)**，預設值是 NULL。 支援萬用字元的模式比對。  
  
 [  **@sp_owner =** ] **'***結構描述***'**  
 這是程序所屬的結構描述名稱。 *結構描述*是**nvarchar(384)**，預設值是 NULL。 支援萬用字元的模式比對。 如果*擁有者*未指定，套用基礎 dbms 的預設程序可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前結構描述含有指定名稱的程序，就會傳回該程序。 如果指定的是非限定的預存程序，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會以下列順序搜尋該程序：  
  
-   目前資料庫的 **sys** 結構描述。  
  
-   如果在批次或動態 SQL 中執行，則為呼叫端的預設結構描述；或者，如果非限定程序名稱出現在另一個程序定義的內文裡面，接下來就會搜尋含有這個其他程序的結構描述。  
  
-   目前資料庫中的 **dbo** 結構描述。  
  
 [  **@qualifier =** ] **'***限定詞***'**  
 這是程序限定詞的名稱。 *限定詞*是**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分的表單中的資料表命名 (*限定詞 ***。*** 結構描述 ***。*** 名稱*。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，*限定詞*代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [  **@fUsePattern =** ] **'***fUsePattern***'**  
 決定是否將底線 (_)、百分比 (%) 或方括號 ([ ]) 視為萬用字元。 *fUsePattern*是**元**，預設值是 1。  
  
 **0** = 模式比對已關閉。  
  
 **1** = 模式比對不上。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|程序限定詞名稱。 這個資料行可以是 NULL。|  
|**PROCEDURE_OWNER**|**sysname**|程序擁有者名稱。 這個資料行一律會傳回值。|  
|**程序名稱**|**nvarchar(134)**|程序名稱。 這個資料行一律會傳回值。|  
|**NUM_INPUT_PARAMS**|**int**|保留供日後使用。|  
|**NUM_OUTPUT_PARAMS**|**int**|保留供日後使用。|  
|**NUM_RESULT_SETS**|**int**|保留供日後使用。|  
|**註解**|**varchar(254)**|程序的描述。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|**PROCEDURE_TYPE**|**smallint**|程序類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一定會傳回 2.0。 這個值可以是下列其中一個值：<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>備註  
 為了將互通性提升到最高點，閘道用戶端應該只會採用 SQL 標準模式比對 (百分比 (%) 和底線 (_) 萬用字元)。  
  
 不一定會檢查有關目前使用者特定預存程序執行權的權限資訊；因此，不保證一定能夠存取。 請注意，它只接受三部分名稱。 也就是說，當它們對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行時，只會傳回本機預存程序 (而非採用四部分名稱的遠端預存程序)。 如果伺服器屬性 ACCESSIBLE_SPROC 是 Y 的結果集**sp_server_info**，會傳回只預存程序目前的使用者可以執行。  
  
 **sp_stored_procedures**相當於**SQLProcedures** ODBC 中。 傳回的結果會依照**PROCEDURE_QUALIFIER**， **PROCEDURE_OWNER**，和**PROCEDURE_NAME**。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. 傳回目前資料庫中的所有預存程序  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的所有預存程序。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. 傳回單一預存程序  
 下列範例會傳回 `uspLogError` 預存程序的結果集。  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
