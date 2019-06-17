---
title: sp_marksubscriptionvalidation & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aad2574457285208b47af26d0729c725a22c05b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629187"
---
# <a name="spmarksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將目前開啟交易標示成指定訂閱者的訂閱層級驗證交易。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*是 sysname，沒有預設值。  
  
`[ @destination_db = ] 'destination_db'` 是目的地資料庫的名稱。 *destination_db*已**sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'` 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應該用於所屬的發行集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_marksubscriptionvalidation**用於異動複寫中。  
  
 **sp_marksubscriptionvalidation**不支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者，您無法執行**sp_marksubscriptionvalidation**從明確交易內。 這是因為在用來存取發行者的連結伺服器連接上，不支援使用明確的交易。  
  
 **sp_marksubscriptionvalidation**必須一起搭配使用[sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)，指定值**1**如*subscription_level*，而且可以搭配其他呼叫**sp_marksubscriptionvalidation**來標示其他訂閱者目前開啟的交易。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_marksubscriptionvalidation**。  
  
## <a name="example"></a>範例  
 下列查詢適用於發行資料庫，以用來封裝訂閱層級的驗證命令。 這些命令由指定訂閱者的散發代理程式所收取。 請注意，第一項交易會驗證 '**art1**'，第二個交易會驗證'**art2**'。 也請注意，呼叫**sp_marksubscriptionvalidation**並[sp_article_validation &#40;-&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)已封裝在交易中。 我們建議您只有一個呼叫[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)每筆交易。 這是因為[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)對來源資料表在交易期間保持共用的資料表鎖定。 您應該盡量縮短交易時間，盡可能使其同時發生。  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
