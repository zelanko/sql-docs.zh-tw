---
title: sp_dbmmonitorupdate (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8ee54383074e624d082d2ab782d6b038fd03d06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817057"
---
# <a name="spdbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個鏡像資料庫插入新資料表資料列以更新資料庫鏡像監視狀態資料表，並截斷比目前保留期限舊的資料列。 預設的保留期限為 7 天 (168 小時)。 更新資料表時**sp_dbmmonitorupdate**評估效能計量。  
  
> [!NOTE]  
>  第一次**sp_dbmmonitorupdate**執行時，它會建立資料庫鏡像狀態資料表並**dbm_monitor**固定的資料庫角色中**msdb**資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要為其更新鏡像狀態的資料庫名稱。 如果*database_name*未指定，程序會更新狀態資料表，每個鏡像資料庫的伺服器執行個體。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_dbmmonitorupdate**內容中，才可以執行**msdb**資料庫。  
  
 如果狀態資料表的資料行不適用於夥伴的角色，則在該夥伴上這個值為 NULL。 如果沒有相關資訊可用 (例如在容錯移轉或伺服器重新啟動期間)，則資料行也會具有 NULL 值。  
  
 在後**sp_dbmmonitorupdate**會建立**dbm_monitor**固定的資料庫角色中**msdb**資料庫，成員**sysadmin**固定的伺服器角色可以新增任何使用者到**dbm_monitor**固定的資料庫角色。 **Dbm_monitor**角色可讓其成員，以檢視資料庫鏡像狀態，但不是加以更新，但無法檢視或設定資料庫鏡像事件。  
  
 更新資料庫的鏡像狀態時**sp_dbmmonitorupdate**檢查最新的值已指定的任何鏡像效能標準的警告臨界值。 如果該值超過臨界值，此程序就會在事件記錄檔中新增參考事件。 所有速率都是上一次更新後的平均值。 如需詳細資訊，請參閱 [使用鏡像效能標準的警告臨界值與警示 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例只更新 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的鏡像狀態。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
