---
description: sp_registercustomresolver (Transact-SQL)
title: sp_registercustomresolver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bd973ace7e8edbd7a5ec561fd53a19f8a7a05a92
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543159"
---
# <a name="sp_registercustomresolver-transact-sql"></a>sp_registercustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  登錄在合併式複寫同步處理期間所能叫用的商務邏輯處理常式或 COM 型自訂解析程式。 這個預存程序執行於散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @article_resolver = ] 'article_resolver'` 指定要註冊之自訂商務邏輯的易記名稱。 *article_resolver* 是 **Nvarchar (255) **，沒有預設值。  
  
`[ @resolver_clsid = ] 'resolver_clsid'` 指定要註冊之 COM 物件的 CLSID 值。 自訂商務邏輯 *resolver_clsid* 是 **Nvarchar (50) **，預設值是 Null。 當登錄商務邏輯處理常式組件時，這個參數必須設為有效的 CLSID 或設為 NULL。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly'` 指定要註冊的自訂商務邏輯類型。 *is_dotnet_assembly* 是 **Nvarchar (50) **，預設值是 FALSE。 **true** 表示要註冊的自訂商務邏輯是商務邏輯處理常式元件; **false** 表示它是 COM 元件。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name'` 這是用來執行商務邏輯處理常式的元件名稱。 *dotnet_assembly_name* 是 **Nvarchar (255) **，預設值是 Null。 如果組件未部署在合併代理程式可執行檔的相同目錄、同步啟動合併代理程式之應用程式的相同目錄，或全域組件快取 (GAC) 中，您就必須指定組件的完整路徑。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name'` 這是覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 來執行商務邏輯處理常式之類別的名稱。 名稱應該在 **Namespace**格式的表單中指定。 *dotnet_class_name* 是 **Nvarchar (255) **，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_registercustomresolver** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_registercustomresolver**。  
  
## <a name="see-also"></a>另請參閱  
 [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [針對合併發行項執行自訂衝突解決器](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
