---
title: "檢查點 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs: TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
caps.latest.revision: "59"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6353bd534827ff9066bd7b184a09d67b5867c3cb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在您目前所連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中產生手動檢查點。  
  
> [!NOTE]  
>  如需不同類型的資料庫檢查點和檢查點作業的一般資訊，請參閱[資料庫檢查點 &#40;SQL Server &#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>引數  
 *checkpoint_duration*  
 指定所需要之手動檢查點作業完成的時間 (以秒為單位)。 當*checkpoint_duration*指定，則[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]嘗試執行要求的持續時間內的檢查點。 *Checkpoint_duration*必須是類型的運算式**int** ，而且必須是大於零。 如果省略此參數，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會調整檢查點持續時間，將資料庫應用程式所受到的效能影響降到最低。 *checkpoint_duration*是進階的選項。  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>影響檢查點作業持續時間的因素  
 一般而言，檢查點作業必須寫入的中途分頁數愈多，檢查點作業所需要的時間也會愈長。 為能將其他應用程式所受到的效能影響降到最低，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設會調整檢查點作業執行的寫入頻率。 降低寫入頻率會增加完成檢查點作業所需要的時間。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用此策略的手動檢查點，除非*checkpoint_duration* CHECKPOINT 命令中指定的值。  
  
 使用的效能影響*checkpoint_duration*中途分頁數、 系統以及指定的實際持續時間上的活動數目而定。 例如，如果檢查點通常會在 120 秒內完成，則指定*checkpoint_duration*的 45 秒，會造成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]投入更多資源到非預設所指派的檢查點。 相較之下，指定*checkpoint_duration*為 180 秒會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指派低於預設所指派的資源。 一般而言，簡短*checkpoint_duration*會增加資源專門用來檢查點，長*checkpoint_duration*會減少資源專門用來檢查點。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律會盡其所能地完成檢查點，並會在檢查點完成時，立即傳回 CHECKPOINT 陳述式。 因此，在某些情況下，檢查點作業的完成會比指定的持續時間快，執行時間也有可能超出指定的持續時間。  
  
##  <a name="Security"></a> 安全性  
  
### <a name="permissions"></a>Permissions  
 CHECKPOINT 權限的成員預設**sysadmin**固定的伺服器角色和**db_owner**和**db_backupoperator**固定資料庫角色，且不可轉移。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [資料庫檢查點 &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [設定 recovery interval 伺服器組態選項](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
