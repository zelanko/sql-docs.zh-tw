---
description: sp_marksubscriptionvalidation (Transact-SQL)
title: sp_marksubscriptionvalidation (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1046bf396112309e17752088969c9556b50ae1cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464142"
---
# <a name="sp_marksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'` 這是訂閱者的名稱。 *訂閱者* 是 sysname，沒有預設值。  
  
`[ @destination_db = ] 'destination_db'` 這是目的地資料庫的名稱。 *destination_db* 是 **sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *發行者* 不能用於屬於發行者的發行集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_marksubscriptionvalidation** 用於異動複寫中。  
  
 **sp_marksubscriptionvalidation** 不支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果是非發行者，則無法從明確的交易中執行**sp_marksubscriptionvalidation** 。 這是因為在用來存取發行者的連結伺服器連接上，不支援使用明確的交易。  
  
 **sp_marksubscriptionvalidation**必須與[sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)搭配使用，並針對*subscription_level*指定**1**的值，而且可以與其他**sp_marksubscriptionvalidation**呼叫一起使用，以標記其他訂閱者目前的開啟交易。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_marksubscriptionvalidation**。  
  
## <a name="example"></a>範例  
 下列查詢適用於發行資料庫，以用來封裝訂閱層級的驗證命令。 這些命令由指定訂閱者的散發代理程式所收取。 請注意，第一個交易會驗證發行項 '**art1**'，而第二個交易則會驗證 '**art2**'。 另請注意， **sp_marksubscriptionvalidation** 和 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 的呼叫已封裝在交易中。 我們建議您對每一筆交易 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 的單一呼叫。 這是因為 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 在交易期間保留來源資料表上的共用資料表鎖定。 您應該盡量縮短交易時間，盡可能使其同時發生。  
  
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
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
