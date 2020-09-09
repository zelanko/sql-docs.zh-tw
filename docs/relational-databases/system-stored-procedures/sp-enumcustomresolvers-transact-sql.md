---
description: sp_enumcustomresolvers (Transact-SQL)
title: sp_enumcustomresolvers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2971d44f61076191addb74a701bb03069d06bc4c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549750"
---
# <a name="sp_enumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回所有可用的商務邏輯處理常式，以及在散發者端登錄的自訂解析程式清單。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>引數  
`[ @distributor = ] 'distributor'` 這是自訂解析程式所在的散發者名稱。 散發者是**sysname**，預設*值是 Null* 。 *這個參數已被取代，未來的版本將會移除它。*  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar(255)**|商務邏輯處理常式或衝突解析程式的易記名稱。|  
|**resolver_clsid**|**nvarchar(50)**|COM 型解析程式的類別識別碼 (CLSID)。 如果是商務邏輯處理常式，這個資料行會傳回零 CLSID 值。|  
|**is_dotnet_assembly**|**bit**|指出是否為商務邏輯處理常式的登錄。<br /><br /> **0** = 以 COM 為基礎的衝突解決器<br /><br /> **1** = 商務邏輯處理常式|  
|**dotnet_assembly_name**|**nvarchar(255)**|實作商務邏輯處理常式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件的名稱。|  
|**dotnet_class_name**|**nvarchar(255)**|這是覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 來實作商務邏輯處理常式的類別名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_enumcustomresolvers** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色和 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_enumcustomresolvers**。  
  
## <a name="see-also"></a>另請參閱  
 [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [針對合併發行項執行自訂衝突解決器](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
