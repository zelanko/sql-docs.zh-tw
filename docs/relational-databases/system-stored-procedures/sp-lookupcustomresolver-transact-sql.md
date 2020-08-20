---
description: sp_lookupcustomresolver (Transact-SQL)
title: sp_lookupcustomresolver (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 75f030013417d3cb5f68f8349d36cb26f9971a88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473948"
---
# <a name="sp_lookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @article_resolver = ] 'article_resolver'` 指定要取消註冊之自訂商務邏輯的名稱。 *article_resolver* 是 **Nvarchar (255) **，沒有預設值。 如果移除的商務邏輯是 COM 元件，這個參數就是元件的易記名稱。 如果商務邏輯是一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件，這個參數就是組件的名稱。  
  
`[ @resolver_clsid = ] 'resolver_clsid' OUTPUT` 這是與 *article_resolver* 參數中所指定的自訂商務邏輯名稱相關聯之 COM 物件的 CLSID 值。 *resolver_clsid* 是 **Nvarchar (50) **，預設值是 Null。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly' OUTPUT` 指定要註冊的自訂商務邏輯類型。 *is_dotnet_assembly* 是 **bit**，預設值是0。 **1** 表示要註冊的自訂商務邏輯是商務邏輯處理常式元件; **0** 表示它是 COM 元件。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT` 這是用來執行商務邏輯處理常式的元件名稱。 *dotnet_assembly_name* 是 **Nvarchar (255) **，預設值是 Null。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT` 這是覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 來執行商務邏輯處理常式之類別的名稱。 *dotnet_class_name* 是 **Nvarchar (255) **，預設值是 Null。  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。 當並未從發行者呼叫預存程序時，請使用這個參數。 若未指定，就假設本機伺服器是發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_lookupcustomresolver** 用於合併式複寫中。  
  
 當註冊所屬的 .NET Framework 元件註冊為商務邏輯處理常式時， **sp_lookupcustomresolver**會傳回*resolver_clsid*的 Null 值（當元件未在散發時註冊時）和值 "00000000-0000-0000-0000-000000000000"。  
  
 **sp_lookupcustomresolver** 是由 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 呼叫，以驗證指定的 *article_resolver*。  
  
## <a name="permissions"></a>權限  
 只有發行集資料庫上 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_lookupcustomresolver**。  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [在合併同步處理期間執行商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [指定合併發行項解析程式](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
