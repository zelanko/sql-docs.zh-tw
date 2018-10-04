---
title: sp_replmonitorsubscriptionpendingcmds & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 432b95c4c19e47dc1df6ffd2273a3163a8d860d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799776"
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回對於交易式發行集的訂閱之暫止命令數目的相關資訊，以及處理它們需要大約多少時間的概略估計。 這個預存程序會針對每項傳回的訂閱，各傳回一個資料列。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher** = ] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 這是發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [ **@publication** = ] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [ **@subscriber** = ] **'***subscriber***'**  
 這是訂閱者的名稱。 *訂閱者*已**sysname**，沒有預設值。  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*已**sysname**，沒有預設值。  
  
 [ **@subscription_type** =] *subscription_type*  
 若是訂閱的類型。 *publication_type*已**int**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|發送訂閱|  
|**1**|提取訂閱|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|訂閱的暫止命令數目。|  
|**estimatedprocesstime**|**int**|估計將所有暫止命令傳遞給訂閱者所需要的秒數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorsubscriptionpendingcmds**用於異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者端**db_owner**散發資料庫中的固定的資料庫角色可以執行**sp_replmonitorsubscriptionpendingcmds**。 發行集存取清單成員可以執行使用散發資料庫的發行集**sp_replmonitorsubscriptionpendingcmds**傳回暫止這個發行集的命令。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
