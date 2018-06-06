---
title: sp_table_validation (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d82517f09ad18c7cc0b2e8d49acfdae6ab200ee9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

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
 [  **@table=**] **'***資料表***'**  
 這是資料表的名稱。 *資料表*是**sysname**，沒有預設值。  
  
 [  **@expected_rowcount=**] *expected_rowcount*輸出  
 指定是否傳回資料表中的預期資料列數。 *expected_rowcount*是**int**，預設值是 NULL。 如果是 NULL，就會在輸出參數中傳回實際的資料列計數。 如果提供了值，就會針對實際資料列計數來檢查值，以識別任何差異。  
  
 [  **@expected_checksum=**] *expected_checksum*輸出  
 指定是否要傳回資料表中的預期總和檢查碼。 *expected_checksum*是**數值**，預設值是 NULL。 如果是 NULL，就會在輸出參數中傳回實際的總和檢查碼。 如果提供了值，就會針對實際總和檢查碼來檢查值，以識別任何差異。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定要執行的總和檢查碼或資料列計數類型。 *type_of_check_requested*是**smallint**，預設值是**1**。  
  
 如果**0**，執行資料列計數和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容總和檢查碼。  
  
 如果**1**，執行資料列計數檢查。  
  
 如果**2**，執行資料列計數及二進位總和檢查碼。  
  
 [  **@owner=**] **'***擁有者***'**  
 這是資料表擁有者的名稱。 *擁有者*是**sysname**，預設值是 NULL。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 這是用於計算資料列計數的方法。 *full_or_fast*是**tinyint**，預設值是**2**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|快速計數從**sysindexes.rows**。 計算的資料列**sysindexes**比計算實際資料表中的資料列快得多。 不過，因為**sysindexes**是延遲的方式更新，資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果*expected_rowcount*為 NULL，而且預存程序正用於取得值，請完整 COUNT(*) 一律使用。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 如果散發代理程式正在執行**sp_table_validation**，指定是否散發代理程式應該立即關閉驗證完成時。 *shutdown_agent*是**元**，預設值是**0**。 如果**0**，複寫代理程式不會關機。 如果**1**、 產生 20578 錯誤和複寫代理程式收到關閉信號。 這個參數已忽略時**sp_table_validation**由使用者直接執行。  
  
 [  **@table_name =**] *table_name*  
 這是輸出訊息所用之檢視的資料表名稱。 *table_name*是**sysname**，預設值是**@table**。  
  
 [ **@column_list**=] **'***column_list***'**  
 這是總和檢查碼函數所應使用之資料行的清單。 *column_list*是**nvarchar （4000)**，預設值是 NULL。 啟用合併發行項驗證來指定排除計算和時間戳記資料行的資料行清單。  
  
## <a name="return-code-values"></a>傳回碼值  
 如果執行總和檢查碼驗證和預期的總和檢查碼等於資料表中的總和檢查碼**sp_table_validation**傳回資料表通過總和檢查碼驗證的訊息。 否則，它會傳回一則訊息來說明資料表可能不會同步處理，且會報告預期資料列數和實際資料列數的差異。  
  
 如果執行資料列計數驗證和預期的資料列數目等於資料表中的數字**sp_table_validation**傳回資料表通過資料列計數驗證的訊息。 否則，它會傳回一則訊息來說明資料表可能不會同步處理，且會報告預期資料列數和實際資料列數的差異。  
  
## <a name="remarks"></a>備註  
 **sp_table_validation**用於所有複寫類型。 **sp_table_validation**不支援 Oracle 發行者。  
  
 總和檢查碼會在頁面的整個資料列影像上，計算 32 位元的循環冗餘檢查 (CRC)。 它不會選擇性地檢查資料行，也不會處理資料表的檢視或垂直資料分割。 此外，總和檢查碼會略過的內容**文字**和**映像**（符合設計） 的資料行。  
  
 當執行總和檢查碼時，兩部伺服器的資料表結構必須相同；也就是說，資料表必須有相同順序、資料類型和長度，以及 NULL/NOT NULL 狀況的相同資料行。 例如，如果發行者執行 CREATE TABLE，再執行 ALTER TABLE 來加入資料行，但訂閱者端所套用的指令碼是簡單 CREATE 資料表，結構就不同。 如果您不確定兩個資料表的結構是完全相同，請查看[syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)並確認每個資料表中的位移相同。  
  
 浮點值可能會產生總和檢查碼差異如果使用字元模式**bcp**被使用，也就是發行集有非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 訂閱者 」。 這些是在轉換成字元模式，或從字元模式轉換時，因有效位數的次要和無法避免的差異所造成的。  
  
## <a name="permissions"></a>Permissions  
 若要執行**sp_table_validation**，您必須有所驗證之資料表上具有 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [總和檢查碼&#40;Transact SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
