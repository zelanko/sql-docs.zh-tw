---
title: sp_article_validation & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f0d205f22e00916c53f5557458694d939bf1766
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210907"
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
 [  **@publication=**] **'**_發行集_**'**  
 這是發行項所在發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=**] **'**_文章_**'**  
 這是要驗證的發行項名稱。 *發行項*已**sysname**，沒有預設值。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定是否只傳回資料表的資料列計數。 *type_of_check_requested*已**smallint**，預設值是**1**。  
  
 如果**0**，執行資料列計數並[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容總和檢查碼。  
  
 如果**1**，執行資料列計數檢查。  
  
 如果**2**，執行資料列計數及二進位總和檢查碼。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 這是用於計算資料列計數的方法。 *full_or_fast*已**tinyint**，而且可以是下列值之一。  
  
|**值**|**說明**|  
|---------------|---------------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|執行快速計數**sysindexes.rows**。 計算資料列**sysindexes**速度，比計算實際資料表中的資料列。 不過， **sysindexes**會以延遲的方式，更新和資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果*expected_rowcount*是 NULL，且預存程序正在使用此選項，以取得此值，完整 COUNT(*) 一律會使用。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 指定在驗證完成時，是否應該立即關閉散發代理程式。 *shutdown_agent*已**位元**，預設值是**0**。 如果**0**，散發代理程式不會關機。 如果**1**，散發代理程式會在驗證發行項之後關閉。  
  
 [  **@subscription_level=**] *subscription_level*  
 指定是否由一組訂閱者來收取驗證。 *subscription_level*已**位元**，預設值是**0**。 如果**0**，驗證會套用到所有 「 訂閱者 」。 如果**1**，驗證只會套用到訂閱者對所指定的子集**sp_marksubscriptionvalidation**中目前開啟的交易。  
  
 [  **@reserved=**]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@publisher**=] **'**_發行者_**'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*應該不在要求上進行驗證時才使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_article_validation**用於異動複寫中。  
  
 **sp_article_validation**讓指定的發行項上收集驗證資訊與交易記錄檔將驗證要求公佈。 當散發代理程式收到這個要求時，散發代理程式會比較要求中的驗證資訊與訂閱者資料表。 驗證結果會顯示在複寫監視器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示中。  
  
## <a name="permissions"></a>Permissions  
 只有具有使用者選取來源資料表上的所有權限，可以執行發行**sp_article_validation**。  
  
## <a name="see-also"></a>另請參閱  
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
