---
title: sp_lookupcustomresolver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7f1bfc868b34ac16e1c38aedc9193002d35d5b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62959618"
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
`[ @article_resolver = ] 'article_resolver'` 指定要取消登錄的自訂商務邏輯名稱。 *article_resolver*已**nvarchar(255)** ，沒有預設值。 如果移除的商務邏輯是 COM 元件，這個參數就是元件的易記名稱。 如果商務邏輯是一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件，這個參數就是組件的名稱。  
  
`[ @resolver_clsid = ] 'resolver_clsid' OUTPUT` 指定的自訂商務邏輯的名稱相關聯的 COM 物件的 CLSID 值*article_resolver*參數。 *resolver_clsid*已**nvarchar(50)** ，預設值是 NULL。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly' OUTPUT` 指定要登錄的自訂商務邏輯的類型。 *is_dotnet_assembly*已**元**，預設值是 0。 **1**表示要登錄的自訂商務邏輯是商務邏輯處理常式組件。**0**表示它是 COM 元件。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT` 是實作商務邏輯處理常式的組件名稱。 *dotnet_assembly_name*已**nvarchar(255)** ，預設值是 NULL。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT` 覆寫的類別名稱<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>實作商務邏輯處理常式。 *dotnet_class_name*已**nvarchar(255)** ，預設值是 NULL。  
  
`[ @publisher = ] 'publisher'` 是 「 發行者 」 的名稱。 *發行者*已**sysname**，預設值是 NULL。 當並未從發行者呼叫預存程序時，請使用這個參數。 若未指定，就假設本機伺服器是發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_lookupcustomresolver**用於合併式複寫中。  
  
 **sp_lookupcustomresolver**傳回的 NULL 值*resolver_clsid*當元件並未登錄於散發，值是"00000000-0000-0000-0000-000000000000"當登錄屬於.NET framework 組件註冊為商務邏輯處理常式。  
  
 **sp_lookupcustomresolver**會呼叫[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)並[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)來驗證指定*article_resolver*。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**發行集資料庫的固定的資料庫角色可以執行**sp_lookupcustomresolver**。  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [在合併同步處理期間執行商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [指定合併發行項解析程式](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
