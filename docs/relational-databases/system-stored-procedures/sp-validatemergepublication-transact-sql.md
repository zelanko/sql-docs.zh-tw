---
title: sp_validatemergepublication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_validatemergepublication
- sp_validatemergepublication_TSQL
helpviewer_keywords:
- sp_validatemergepublication
ms.assetid: 5a862f1a-2be1-4758-9954-4cdc8c77d149
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e435b66f6267466f0d0ac48eef8a87648ca0dd94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spvalidatemergepublication-transact-sql"></a>sp_validatemergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行全發行集的驗證，所有訂閱 (發送、提取和匿名) 都要驗證一次。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>引數  
 [**@publication=**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@level=** ]*層級*  
 這是要執行的類型驗證。 *層級*是**tinyint**，沒有預設值。 層級可以是下列值之一。  
  
|層級值|Description|  
|-----------------|-----------------|  
|**1**|僅驗證資料列計數。|  
|**2**|資料列計數及總和檢查碼驗證。 如[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]「 訂閱者 」，這會自動設為**3**。|  
|**3**|這是建議值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_validatemergepublication**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_validatemergepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_validatemergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
