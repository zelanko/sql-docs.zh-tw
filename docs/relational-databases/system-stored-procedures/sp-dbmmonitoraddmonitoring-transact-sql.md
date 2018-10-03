---
title: sp_dbmmonitoraddmonitoring (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a4850b86366a74b0b65b6acddd334960ec12096
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615556"
---
# <a name="spdbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 如果從啟動資料庫鏡像[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，則**sp_dbmmonitoraddmonitoring**程序就會自動執行。 如果您啟動鏡像功能的設定使用 ALTER DATABASE 陳述式，以手動方式，來監視鏡像的資料庫的伺服器執行個體中，您必須執行**sp_dbmmonitoraddmonitoring**以手動方式。  
  
> [!NOTE]  
>  如果您執行**sp_dbmmonitoraddmonitoring**設定資料庫鏡像之前，監視作業會執行，但不是會更新狀態資料表的資料庫中儲存鏡像監視記錄。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例使用 `3` 分鐘的更新週期開始進行監視。  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
