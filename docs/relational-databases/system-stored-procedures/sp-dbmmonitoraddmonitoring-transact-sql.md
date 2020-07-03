---
title: sp_dbmmonitoraddmonitoring （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitoraddmonitoring
- sp_dbmmonitoraddmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitoraddmonitoring
ms.assetid: 9489dc30-af29-4363-a172-4645947fc95e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 268226d28b134ffe13a5acfca3baf47bde655baf
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85866740"
---
# <a name="sp_dbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  建立資料庫鏡像監視作業，以定期更新伺服器執行個體上每個鏡像資料庫的鏡像狀態。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitoraddmonitoring [ update_period ]  
```  
  
## <a name="arguments"></a>引數  
 *update_period*  
 以分鐘數指定更新之間的間隔。 這個值可以介於 1 和 120 分鐘之間。 預設值是 1 分鐘。  
  
> [!NOTE]  
>  如果更新週期的設定值過低，則用戶端的回應時間可能會增加。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這項程序要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 必須能在伺服器執行個體上執行，而且若要執行資料庫鏡像監視作業，就必須執行代理程式。  
  
 如果從啟動資料庫鏡像 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，則會自動執行**sp_dbmmonitoraddmonitoring**程式。 如果您使用 ALTER DATABASE 語句來手動啟動鏡像，以監視伺服器實例上的鏡像資料庫，您必須手動執行**sp_dbmmonitoraddmonitoring** 。  
  
> [!NOTE]  
>  如果您在設定資料庫鏡像之前執行**sp_dbmmonitoraddmonitoring** ，監視作業將會執行，但不會更新儲存資料庫鏡像監視器記錄的狀態資料表。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例使用 `3` 分鐘的更新週期開始進行監視。  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
