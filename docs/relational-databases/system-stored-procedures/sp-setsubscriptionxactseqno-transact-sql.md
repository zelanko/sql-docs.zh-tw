---
title: sp_setsubscriptionxactseqno （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27a7f35a915e2bff62932124aef64984a63cbd0e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68021080"
---
# <a name="sp_setsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在疑難排解期間使用，以指定使用記錄序號（LSN）的上次傳遞交易，讓散發代理程式在下一次交易時開始傳遞。 重新開機時，散發代理程式會從散發資料庫快取（msrepl_commands）傳回大於此浮水印（LSN）的交易。 這個預存程序執行於訂閱資料庫的訂閱者端。 不支援非 SQL Server 訂閱者使用這個項目。  
  
> [!CAUTION]  
>  不正確使用這個預存程序或指定了不正確的 LSN 值，散發代理程式可能會還原訂閱者端先前所套用的變更，也可能會略過所有其餘變更。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。 若為非 SQL Server 的發行者， *publisher_db*是散發資料庫的名稱。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。 當散發代理程式由一個以上的發行集共用時，您必須為*發行*集指定 ALL 的值。  
  
`[ @xact_seqno = ] xact_seqno`這是要在「訂閱者」端套用之「散發者」端下一個交易的 LSN。 *xact_seqno*是**Varbinary （16）**，沒有預設值。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|訂閱者端所要套用之下一項交易的原始 LSN。|  
|**UPDATED XACT_SEQNO**|**varbinary(16)**|訂閱者端所要套用之下一項交易的更新 LSN。|  
|**SUBSCRIPTION STREAM COUNT**|**int**|在上一次同步處理期間所用的訂閱資料流數目。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_setsubscriptionxactseqno**用於異動複寫中。  
  
 **sp_setsubscriptionxactseqno**不能用在點對點事務複寫拓撲中。  
  
 **sp_setsubscriptionxactseqno**可以用來略過在訂閱者端套用時，會造成錯誤的特定交易。 當發生失敗，且在散發代理程式停止之後，請在散發者端呼叫[sp_helpsubscriptionerrors &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) ，以取得失敗交易的 xact_seqno 值，然後呼叫**sp_setsubscriptionxactseqno**，傳遞此值給*xact_seqno*。 這可以確保只會處理在這個 LSN 之後的命令。  
  
 為*xact_seqno*指定**0**的值，以將散發資料庫中的所有暫止命令傳遞給訂閱者。  
  
 如果散發代理程式使用多個訂用帳戶串流， **sp_setsubscriptionxactseqno**可能會失敗。  
  
 當發生這個錯誤時，您必須利用單一訂閱資料流來執行散發代理程式。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_setsubscriptionxactseqno**。  
  
## <a name="see-more"></a>查看更多

[Blog：如何略過交易](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  
