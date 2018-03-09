---
title: "sp_replmonitorsubscriptionpendingcmds (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c135e779e1d1f6fd0b5da12f3b9a24f2ade96eea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 [  **@publisher**  =] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 這是發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [  **@publication**  =] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@subscriber**  =] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
 [  **@subscriber_db**  =] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，沒有預設值。  
  
 [  **@subscription_type**  =] *subscription_type*  
 若是訂閱的類型。 *publication_type*是**int**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|發送訂閱|  
|**1**|提取訂閱|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|訂閱的暫止命令數目。|  
|**estimatedprocesstime**|**int**|估計將所有暫止命令傳遞給訂閱者所需要的秒數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorsubscriptionpendingcmds**異動複寫搭配使用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者**db_owner**散發資料庫中的固定的資料庫角色可以執行**sp_replmonitorsubscriptionpendingcmds**。 發行集存取清單成員可以執行使用散發資料庫的發行集**sp_replmonitorsubscriptionpendingcmds**傳回暫止這個發行集的命令。  
  
## <a name="see-also"></a>請參閱＜  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
