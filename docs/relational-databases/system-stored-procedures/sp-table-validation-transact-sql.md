---
description: sp_table_validation (Transact-SQL)
title: sp_table_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 88ee13025153fff3018fadfa8d64becf7a534303
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545918"
---
# <a name="sp_table_validation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  傳回資料表或索引檢視的資料列計數或總和檢查碼資訊，或利用指定的資料表或索引檢視來比較提供的資料列計數或總和檢查碼資訊。 這個預存程序執行於發行集資料庫的發行者端，以及訂閱資料庫的訂閱者端。 *不支援 Oracle 發行者*。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table = ] 'table'` 這是資料表的名稱。 *table* 是 **sysname**，沒有預設值。  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` 指定是否傳回資料表中預期的資料列數目。 *expected_rowcount* 是 **int**，預設值是 Null。 如果是 NULL，就會在輸出參數中傳回實際的資料列計數。 如果提供了值，就會針對實際資料列計數來檢查值，以識別任何差異。  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` 指定是否傳回資料表的預期總和檢查碼。 *expected_checksum* 是 **數值**，預設值是 Null。 如果是 NULL，就會在輸出參數中傳回實際的總和檢查碼。 如果提供了值，就會針對實際總和檢查碼來檢查值，以識別任何差異。  
  
`[ @rowcount_only = ] type_of_check_requested` 指定要執行的總和檢查碼或資料列計數類型。 *type_of_check_requested* 是 **Smallint**，預設值是 **1**。  
  
 如果是 **0**，則執行資料列計數和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容的總和檢查碼。  
  
 如果是 **1**，則只執行資料列計數檢查。  
  
 如果是 **2**，則執行資料列計數和二進位總和檢查碼。  
  
`[ @owner = ] 'owner'` 這是資料表擁有者的名稱。 *owner* 是 **sysname**，預設值是 Null。  
  
`[ @full_or_fast = ] full_or_fast` 這是用來計算資料列計數的方法。 *full_or_fast* 是 **Tinyint**，預設值是 **2**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|從 **sysindexes**快速算算。 計算 **sysindexes** 中的資料列比計算實際資料表中的資料列更快。 不過，因為 **sysindexes** 延遲更新，所以資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果 *expected_rowcount* 為 Null，且使用預存程式來取得值，就一律會使用完整的計數 ( * ) 。|  
  
`[ @shutdown_agent = ] shutdown_agent` 如果散發代理程式正在執行 **sp_table_validation**，指定是否應在驗證完成時立即關閉散發代理程式。 *shutdown_agent* 是 **bit**，預設值是 **0**。 如果是 **0**，複寫代理程式就不會關閉。 如果是 **1**，則會引發錯誤20578，並將複寫代理程式告知關閉。 當使用者直接執行 **sp_table_validation** 時，會忽略這個參數。  
  
`[ @table_name = ] table_name` 這是用於輸出訊息之視圖的資料表名稱。 *table_name*是**sysname**，預設值是** \@ table**。  
  
`[ @column_list = ] 'column_list'` 這是總和檢查碼函數中所應使用的資料行清單。 *column_list* 是 **Nvarchar (4000) **，預設值是 Null。 啟用合併發行項驗證來指定排除計算和時間戳記資料行的資料行清單。  
  
## <a name="return-code-values"></a>傳回碼值  
 如果執行總和檢查碼驗證，且預期的總和檢查碼等於資料表中的總和檢查碼， **sp_table_validation** 會傳回一則訊息，表示資料表已通過總和檢查碼驗證。 否則，它會傳回一則訊息來說明資料表可能不會同步處理，且會報告預期資料列數和實際資料列數的差異。  
  
 如果執行資料列計數驗證，且預期的資料列數目等於資料表中的數位， **sp_table_validation** 會傳回一則訊息，表示資料表已傳遞了資料列計數驗證。 否則，它會傳回一則訊息來說明資料表可能不會同步處理，且會報告預期資料列數和實際資料列數的差異。  
  
## <a name="remarks"></a>備註  
 **sp_table_validation** 用於所有類型的複寫中。 Oracle 發行者不支援**sp_table_validation** 。  
  
 總和檢查碼會在頁面的整個資料列影像上，計算 32 位元的循環冗餘檢查 (CRC)。 它不會選擇性地檢查資料行，也不會處理資料表的檢視或垂直資料分割。 此外，總和檢查碼也會略過設計)  (的 **text** 和 **image** 資料行內容。  
  
 當執行總和檢查碼時，兩部伺服器的資料表結構必須相同；也就是說，資料表必須有相同順序、資料類型和長度，以及 NULL/NOT NULL 狀況的相同資料行。 例如，如果發行者執行 CREATE TABLE，再執行 ALTER TABLE 來加入資料行，但訂閱者端所套用的指令碼是簡單 CREATE 資料表，結構就不同。 如果您不確定兩個數據表的結構完全相同，請查看 [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) ，並確認每個資料表中的位移都相同。  
  
 如果使用字元模式 **bcp** ，浮點值可能會產生總和檢查碼差異，如果發行集有非訂閱者，則為這種情況 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些是在轉換成字元模式，或從字元模式轉換時，因有效位數的次要和無法避免的差異所造成的。  
  
## <a name="permissions"></a>權限  
 若要執行 **sp_table_validation**，您必須具有要驗證之資料表的 SELECT 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [CHECKSUM &#40;Transact-sql&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
