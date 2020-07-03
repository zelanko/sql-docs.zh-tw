---
title: sp_scriptsubconflicttable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 93656ff6bec2acc3c3f6f7ee189b1c45db75a7d6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899195"
---
# <a name="sp_scriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  產生針對給定的佇列訂閱發行項，在訂閱者上建立一份衝突資料表的指令碼。 這份產生的指令碼執行於訂閱資料庫的訂閱者端。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是包含發行項的發行集名稱。 這個名稱在資料庫內必須是唯一的。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是訂閱發行項的名稱。 *文章*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|傳回針對給定的佇列訂閱發行項，在訂閱者上建立衝突資料表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 這份指令碼執行於訂閱資料庫的訂閱者端。|  
  
## <a name="remarks"></a>備註  
 **sp_scriptsubconflicttable**用於具有手動套用初始快照集之訂用帳戶的訂閱者。 衝突資料表是訂閱者的一份選擇性資料表。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_scriptsubconflicttable**。  
  
## <a name="see-also"></a>另請參閱  
 [佇列更新衝突偵測和解決](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
