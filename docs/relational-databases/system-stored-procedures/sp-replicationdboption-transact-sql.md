---
title: sp_replicationdboption & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 153c2e2b8c75c21451dca3b673129a059d78e3a6
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527330"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定指定資料庫的複寫資料庫選項。 這個預存程序執行於任何資料庫的發行者端或訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>引數  
 [**@dbname=**] **'***dbname***'**  
 這是要設定複寫資料庫選項的資料庫。 *db_name*已**sysname**，沒有預設值。  
  
 [**@optname=**] **'***optname***'**  
 這是要啟用或停用的複寫資料庫選項。 *optname*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**合併式發行**|可用於合併式發行集的資料庫。|  
|**publish**|資料庫可用於其他類型的發行集。|  
|**subscribe**|資料庫是訂閱資料庫。|  
|**備份與同步處理**|啟用資料庫的協調備份。 如需詳細資訊，請參閱 <<c0> [ 為異動複寫啟用協調備份&#40;Replication TRANSACT-SQL Programming&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)。</c0>|  
  
`[ @value = ] 'value'` 要啟用或停用指定的複寫資料庫選項。 *值*是**sysname**，而且可以是 **，則為 true**或是**false**。 當這個值是**假**並*optname*是**合併式發行**，也會卸除到合併式發行資料庫的訂用帳戶。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否要將此預存程序執行而不需要連線到散發者。 *ignore_distributor*已**位元**，預設值是**0**，表示散發者應該連接到並更新與發行集資料庫的新狀態。 該值**1**才應該指定 「 散發者 」 是否無法存取並**sp_replicationdboption**用來停用發行。  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replicationdboption**用於快照式複寫、 異動複寫和合併式複寫。  
  
 隨著給定的選項而不同，這個程序會建立或卸除特定複寫系統資料表、安全性帳戶等。 設定對應的類別目錄中的位元**master.sysdatabases**系統資料表，並建立必要的系統資料表。  
  
 若要停用發行，發行集資料庫必須在線上。 如果發行集資料庫的資料庫快照集存在，您必須先卸除它，才能停用發行。 資料庫快照集是資料庫的唯讀離線複本，與複寫快照集無關。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_replicationdboption**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [刪除發行集](../../relational-databases/replication/publish/delete-a-publication.md)   
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
