---
title: sp_marksubscriptionvalidation （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: c440247433404c520559d6609bd4690b425ddd43
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899347"
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
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是 sysname，沒有預設值。  
  
`[ @destination_db = ] 'destination_db'`這是目的地資料庫的名稱。 *destination_db*是**sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'`指定非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *發行者*不應用於屬於發行者的發行集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_marksubscriptionvalidation**用於異動複寫中。  
  
 **sp_marksubscriptionvalidation**不支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。  
  
 對於非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者，您無法從明確交易內執行**sp_marksubscriptionvalidation** 。 這是因為在用來存取發行者的連結伺服器連接上，不支援使用明確的交易。  
  
 **sp_marksubscriptionvalidation**必須與[sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)一起使用，針對*subscription_level*指定**1**的值，而且**可以與其他**呼叫一起使用，以對其他訂閱者標記目前開啟的交易。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_marksubscriptionvalidation**。  
  
## <a name="example"></a>範例  
 下列查詢適用於發行資料庫，以用來封裝訂閱層級的驗證命令。 這些命令由指定訂閱者的散發代理程式所收取。 請注意，第一個交易會驗證發行項 '**art1**'，而第二筆交易則會驗證 '**art2**'。 另請注意， **sp_marksubscriptionvalidation**和[sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)的呼叫已封裝在交易中。 我們建議您只在每一筆交易[sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)呼叫一次。 這是因為在交易期間， [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)保存來源資料表的共用資料表鎖定。 您應該盡量縮短交易時間，盡可能使其同時發生。  
  
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
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
