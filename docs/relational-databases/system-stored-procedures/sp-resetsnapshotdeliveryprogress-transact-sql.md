---
title: sp_resetsnapshotdeliveryprogress （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc6205eb5487b89db55488bcdf36fbb036595d57
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129654"
---
# <a name="sp_resetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重設提取訂閱的快照集傳遞處理序，以便重新啟動快照集傳遞。 它是在訂閱資料庫的訂閱者執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @verbose_level = ] verbose_level`指定傳回的資訊量。 *verbose_level*是**int**，預設值是**1**。 值為**1**表示如果無法在**MSsnapshotdeliveryprogress**資料表上取得必要的鎖定，就會傳回錯誤，而**0**表示不會傳回任何錯誤。  
  
`[ @drop_table = ] 'drop_table'`這是指是否要卸載或截斷包含快照集進度資訊的資料表。*drop_table*是**Nvarchar （5）**，預設值是**FALSE**。 False 表示截斷資料表，而 True 表示卸除資料表。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_resetsnapshotdeliveryprogress**移除**MSsnapshotdeliveryprogress**資料表中的所有資料列。 它可以有效移除所有被先前在快照集傳遞處理序所製作的任何進度留在訂閱資料庫的中繼資料。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_resetsnapshotdeliveryprogress**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
