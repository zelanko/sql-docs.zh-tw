---
title: sp_resetsnapshotdeliveryprogress (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 899a590bb2c634568399aca6f5520b52d26a52b4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43022734"
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重設提取訂閱的快照集傳遞處理序，以便重新啟動快照集傳遞。 它是在訂閱資料庫的訂閱者執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@verbose_level**=] *verbose_level*  
 指定傳回的資訊量。 *verbose_level*已**int**，預設值是**1**。 值**1**表示錯誤是傳回如果無法取得必要的鎖定上**MSsnapshotdeliveryprogress**資料表，並**0**表示會傳回任何錯誤。  
  
 [ **@drop_table**=] **'***drop_table***'**  
 要卸除或截斷資料表包含有關進度的快照集。*drop_table*是**nvarchar(5)**，預設值是**FALSE**。 False 表示截斷資料表，而 True 表示卸除資料表。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_resetsnapshotdeliveryprogress**中的所有資料列會移除**MSsnapshotdeliveryprogress**資料表。 它可以有效移除所有被先前在快照集傳遞處理序所製作的任何進度留在訂閱資料庫的中繼資料。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_resetsnapshotdeliveryprogress**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
