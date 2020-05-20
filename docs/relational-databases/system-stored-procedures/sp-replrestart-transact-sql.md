---
title: sp_replrestart （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replrestart_TSQL
- sp_replrestart
helpviewer_keywords:
- sp_replrestart
ms.assetid: 111b3dbf-92f8-4670-b156-1468c63e4fc1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cf58ed6b921c7b83b0b3e6c66a5365e73328c994
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815040"
---
# <a name="sp_replrestart-transact-sql"></a>sp_replrestart (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  在備份與還原期間，供異動複寫使用，以便同步處理散發者端的複寫資料和發行者端的資料。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  **sp_replrestart**是內部複寫預存程式，應該只在還原事務複寫拓撲中發行的資料庫時使用，如[備份與還原快照式和異動複寫的策略](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)中所述。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replrestart  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 當「散發者」端的最高記錄序號（LSN）值不符合「發行者」端的最高 LSN 值時，就會使用**sp_replrestart** 。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_replrestart**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
