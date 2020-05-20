---
title: sp_configure_peerconflictdetection （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_configure_peerconflictdetection_TSQL
- sp_configure_peerconflictdetection
helpviewer_keywords:
- sp_configure_peerconflictdetection
ms.assetid: 45117cb2-3247-433f-ba3d-7fa19514b1c3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a332257b640124c04ed339ff11473b89a7c3b83b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828432"
---
# <a name="sp_configure_peerconflictdetection-transact-sql"></a>sp_configure_peerconflictdetection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對點對點異動複寫拓撲中所包含的發行集設定衝突偵測。 如需相關資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_configure_peerconflictdetection [ @publication = ] 'publication'  
    [ , [ @action = ] 'action']  
    [ , [ @originator_id = ] originator_id ]  
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @continue_onconflict = ] 'continue_onconflict']  
    [ , [ @local = ] 'local']  
    [ , [ @timeout = ] timeout ]  
  
```  
  
## <a name="arguments"></a>引數  
 [ @publication =] '*發行*'  
 這是要設定衝突偵測的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
 [ @action =] '*action*'  
 指定發行集啟用或停用衝突偵測。 *動作*是**Nvarchar （5）**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**enable**|針對發行集啟用衝突偵測。|  
|**disable**|針對發行集停用衝突偵測。|  
|NULL (預設值)||  
  
 [ @originator_id =] *originator_id*  
 針對點對點拓撲中的節點指定識別碼。 *originator_id*是**int**，預設值是 Null。 如果*動作*設定為 [**啟用**]，這個識別碼就會用於衝突偵測。 請指定拓撲中從未使用過的非零正數識別碼。 如需已經使用的識別碼清單，請查詢 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系統資料表。  
  
 [ @conflict_retention =] *conflict_retention*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @continue_onconflict =] '*continue_onconflict*']  
 決定散發代理程式在偵測到衝突之後是否會繼續處理變更。 *continue_onconflict*是**Nvarchar （5）** ，預設值為 FALSE。  
  
> [!CAUTION]  
>  我們建議您使用預設值 FALSE。 當這個選項設定為 TRUE 時，散發代理程式會套用具有最高訂閱者識別碼之節點的衝突資料列，藉以嘗試聚合拓撲中的資料。 但是，這個方法無法保證聚合。 您應該確定在偵測到衝突之後，拓撲是一致的。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。  
  
 [ @local =] '*local*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @timeout =]*超時*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_configure_peerconflictdetection 用於點對點異動複寫中。 若要使用衝突偵測，所有節點都必須 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 執行或更新版本，而且必須針對所有節點啟用偵測。  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [點對點複寫中的衝突偵測](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
