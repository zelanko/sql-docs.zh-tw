---
title: sp_lookupcustomresolver (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad45f26fbd1c6b7f9488497333f5ba44a2b5fa8c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回登錄在散發者端的 COM 型自訂解析程式元件之商務邏輯處理常式或類別識別碼 (CLSID) 值的相關資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 指定要取消註冊之自訂商務邏輯的名稱。 *article_resolver*是**nvarchar （255)**，沒有預設值。 如果移除的商務邏輯是 COM 元件，這個參數就是元件的易記名稱。 如果商務邏輯是一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件，這個參數就是組件的名稱。  
  
 [ **@resolver_clsid**=] **'***resolver_clsid***'**輸出  
 指定的自訂商務邏輯的名稱相關聯之 COM 物件的 CLSID 值*article_resolver*參數。 *resolver_clsid*是**nvarchar （50)**，預設值是 NULL。  
  
 [  **@is_dotnet_assembly=** ] **'***is_dotnet_assembly***'**輸出  
 指定要登錄之自訂商務邏輯的類型。 *is_dotnet_assembly*是**元**，預設值是 0。 **1**表示要登錄的自訂商務邏輯是商務邏輯處理常式組件。**0**表示它是 COM 元件。  
  
 [  **@dotnet_assembly_name=** ] **'***dotnet_assembly_name***'**輸出  
 這是實作商務邏輯處理常式的組件名稱。 *dotnet_assembly_name*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@dotnet_class_name=** ] **'***dotnet_class_name***'**輸出  
 這是覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 來實作商務邏輯處理常式的類別名稱。 *dotnet_class_name*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@publisher=** ] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，預設值是 NULL。 當並未從發行者呼叫預存程序時，請使用這個參數。 若未指定，就假設本機伺服器是發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_lookupcustomresolver**用於合併式複寫中。  
  
 **sp_lookupcustomresolver**傳回 NULL 值的*resolver_clsid*當元件並未登錄於散發，值是"00000000-0000-0000-0000-000000000000"當登錄屬於.NET framework 組件註冊為商務邏輯處理常式。  
  
 **sp_lookupcustomresolver**稱為[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)和[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)來驗證指定*article_resolver*。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**發行集資料庫上的固定的資料庫角色可以執行**sp_lookupcustomresolver**。  
  
## <a name="see-also"></a>另請參閱  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [在合併同步處理期間執行商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [指定合併發行項解析程式](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
