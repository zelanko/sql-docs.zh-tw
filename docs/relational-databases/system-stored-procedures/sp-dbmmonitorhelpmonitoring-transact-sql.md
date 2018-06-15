---
title: sp_dbmmonitorhelpmonitoring (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpmonitoring
- sp_dbmmonitorhelpmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpmonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: a085cf87-269f-454a-a146-21f80a113b72
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a97a85c63a0407d249609251eae63747fed4ad01
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263224"
---
# <a name="spdbmmonitorhelpmonitoring-transact-sql"></a>sp_dbmmonitorhelpmonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前的更新週期。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitorhelpmonitoring   
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 傳回目前的更新週期，也就是資料庫鏡像狀態資料表更新之間的分鐘數。 這個值介於 1 和 120 分鐘之間。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會傳回目前的更新週期。  
  
```  
EXEC sp_dbmmonitorhelpmonitoring;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
