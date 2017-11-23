---
title: "sp_article_validation (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords: sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed9bf6e4375c3b7afb18ffa938ae29e8d1e9e48e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  起始指定發行項的資料驗證要求。 這個預存程序執行於發行集資料庫的發行者端，以及訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=**] **'***發行集***'**  
 這是發行項所在發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是要驗證的發行項名稱。 *發行項*是**sysname**，沒有預設值。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定是否只傳回資料表的資料列計數。 *type_of_check_requested*是**smallint**，預設值是**1**。  
  
 如果**0**，執行資料列計數和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容總和檢查碼。  
  
 如果**1**，執行資料列計數檢查。  
  
 如果**2**，執行資料列計數及二進位總和檢查碼。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 這是用於計算資料列計數的方法。 *full_or_fast*是**tinyint**，而且可以是下列值之一。  
  
|**值**|**說明**|  
|---------------|---------------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|執行快速計數從**sysindexes.rows**。 計算的資料列**sysindexes**的速度比計算實際資料表中的資料列。 不過， **sysindexes**延遲的方式更新和資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果*expected_rowcount*為 NULL，而且預存程序正用於取得值，請完整 COUNT(*) 一律使用。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 指定在驗證完成時，是否應該立即關閉散發代理程式。 *shutdown_agent*是**元**，預設值是**0**。 如果**0**，散發代理程式不會關機。 如果**1**，散發代理程式會在驗證發行項之後關閉。  
  
 [  **@subscription_level=**] *subscription_level*  
 指定是否由一組訂閱者來收取驗證。 *subscription_level*是**元**，預設值是**0**。 如果**0**，驗證會套用到所有 「 訂閱者 」。 如果**1**，驗證只會套用到訂閱者對所指定的子集**sp_marksubscriptionvalidation**中目前開啟的交易。  
  
 [  **@reserved=**]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher** =] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應使用上要求進行驗證時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_article_validation**用於異動複寫中。  
  
 **sp_article_validation**會導致驗證指定的發行項上收集的資訊並公佈到交易記錄檔的驗證要求。 當散發代理程式收到這個要求時，散發代理程式會比較要求中的驗證資訊與訂閱者資料表。 驗證結果會顯示在複寫監視器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示中。  
  
## <a name="permissions"></a>Permissions  
 只有具有使用者能夠執行驗證的發行項，請選取來源資料表上的所有權限**sp_article_validation**。  
  
## <a name="see-also"></a>請參閱＜  
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
