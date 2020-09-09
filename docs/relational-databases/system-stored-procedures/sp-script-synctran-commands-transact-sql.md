---
description: sp_script_synctran_commands (Transact-SQL)
title: sp_script_synctran_commands (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f596a02346748cedcc6b99ada4e0a6122b184673
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541587"
---
# <a name="sp_script_synctran_commands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  產生腳本，其中包含可更新訂閱的訂閱者端所要套用的 **sp_addsynctrigger** 呼叫。 發行集中的每個發行項都有一個 **sp_addsynctrigger** 呼叫。 產生的腳本也包含 **sp_addqueued_artinfo** 呼叫，可建立處理佇列發行集所需的 **MSsubsciption_articles** 資料表。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要編寫腳本的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是要編寫腳本的發行項名稱。 *文章* 是 **sysname**，預設值是 **all**，指定所有發行項的腳本。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="results-set"></a>結果集  
 **sp_script_synctran_commands** 會傳回由單一 **Nvarchar (4000) ** 資料行所組成的結果集。 結果集會形成建立 **sp_addsynctrigger** 以及在訂閱者端套用 **sp_addqueued_artinfo** 呼叫所需的完整腳本。  
  
## <a name="remarks"></a>備註  
 **sp_script_synctran_commands** 用於快照式和異動複寫中。  
  
 **sp_addqueued_artinfo** 用於佇列可更新訂閱。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_script_synctran_commands**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsynctriggers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
