---
title: sp_article_validation （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 6f5ee076163ff3cf0f69daab7ceff115bf5876a6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68769016"
---
# <a name="sp_article_validation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`這是發行項所在的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是要驗證的發行項名稱。 *文章*是**sysname**，沒有預設值。  
  
`[ @rowcount_only = ] type_of_check_requested`指定是否只傳回資料表的資料列計數。 *type_of_check_requested*是**Smallint**，預設值是**1**。  
  
 如果是**0**，則執行資料列[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計數和7.0 相容的總和檢查碼。  
  
 如果是**1**，則只執行資料列計數檢查。  
  
 如果為**2**，則執行資料列計數和二進位總和檢查碼。  
  
`[ @full_or_fast = ] full_or_fast`這是用來計算資料列計數的方法。 *full_or_fast*是**Tinyint**，而且可以是下列其中一個值。  
  
|**ReplTest1**|**說明**|  
|---------------|---------------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|從**sysindexes**執行快速計數。 計算**sysindexes**中的資料列，比計算實際資料表中的資料列快。 不過， **sysindexes**會延遲更新，而且資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果*expected_rowcount*是 Null，而預存程式是用來取得值，則一律會使用完整的 COUNT （*）。|  
  
`[ @shutdown_agent = ] shutdown_agent`指定在驗證完成時，是否應該立即關閉散發代理程式。 *shutdown_agent*是**bit**，預設值是**0**。 如果為**0**，則不會關閉散發代理程式。 如果是**1**，就會在驗證發行項之後關閉散發代理程式。  
  
`[ @subscription_level = ] subscription_level`指定是否由一組訂閱者挑選驗證。 *subscription_level*是**bit**，預設值是**0**。 如果是**0**，則會將驗證套用至所有訂閱者。 如果是**1**，驗證只會套用至目前開啟的交易中**sp_marksubscriptionvalidation**呼叫所指定的訂閱者子集。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *publisher*在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者端要求驗證時，不應使用「發行者」。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_article_validation**用於異動複寫中。  
  
 **sp_article_validation**會在指定的發行項上收集驗證資訊，並將驗證要求張貼至交易記錄。 當散發代理程式收到這個要求時，散發代理程式會比較要求中的驗證資訊與訂閱者資料表。 驗證結果會顯示在複寫監視器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示中。  
  
## <a name="permissions"></a>權限  
 只有在要驗證之發行項的來源資料表上具有 [選取所有] 許可權的使用者，才能執行**sp_article_validation**。  
  
## <a name="see-also"></a>另請參閱  
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
