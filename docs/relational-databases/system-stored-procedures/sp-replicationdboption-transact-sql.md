---
title: "sp_replicationdboption (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
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
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 584c9ed9f4a9d0e00bcbd0de05788a1841189899
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 這是要設定複寫資料庫選項的資料庫。 *db_name*是**sysname**，沒有預設值。  
  
 [**@optname=**] **'***optname***'**  
 這是要啟用或停用的複寫資料庫選項。 *optname*是**sysname**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**合併式發行**|可用於合併式發行集的資料庫。|  
|**發行**|資料庫可用於其他類型的發行集。|  
|**訂閱**|資料庫是訂閱資料庫。|  
|**與備份同步**|啟用資料庫的協調備份。 如需詳細資訊，請參閱[的異動複寫 &#40; 啟用協調備份複寫 TRANSACT-SQL 程式設計 &#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
 [  **@value=**] **'***值***'**  
 這是指要啟用或停用給定的複寫資料庫選項。 *值*是**sysname**，而且可以是**true**或**false**。 當這個值是**false**和*optname*是**合併式發行**，也會卸除合併發行資料庫的訂閱。  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 指出是否在未連接到散發者的情況之下，執行這個預存程序。 *ignore_distributor*是**元**，預設值是**0**，表示散發者應該連接到並更新與發行集資料庫的新狀態。 值**1**才應該指定 「 散發者 」 是否無法存取和**sp_replicationdboption**正用來停用發行。  
  
 [  **@from_scripting=**] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replicationdboption**用於快照式複寫、 異動複寫和合併式複寫。  
  
 隨著給定的選項而不同，這個程序會建立或卸除特定複寫系統資料表、安全性帳戶等。 設定對應的分類中的位元**master.sysdatabases**系統資料表，並建立必要的系統資料表。  
  
 若要停用發行，發行集資料庫必須在線上。 如果發行集資料庫的資料庫快照集存在，您必須先卸除它，才能停用發行。 資料庫快照集是資料庫的唯讀離線複本，與複寫快照集無關。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_replicationdboption**。  
  
## <a name="see-also"></a>請參閱＜  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [刪除發行集](../../relational-databases/replication/publish/delete-a-publication.md)   
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
