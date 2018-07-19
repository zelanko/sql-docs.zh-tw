---
title: sp_bindsession (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7e1654987b889848fdc81f7be273aca10cd1d231
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036226"
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  繫結或解除繫結到相同的執行個體的其他工作階段的工作階段[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 繫結工作階段可讓兩個或更多工作階段參與相同的交易和共用鎖定，直到發出 ROLLBACK TRANSACTION 或 COMMIT TRANSACTION 為止。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用 Multiple Active Result Set (MARS) 或分散式交易。 如需詳細資訊，請參閱 <<c0> [ 使用 Multiple Active Result Sets &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。</c0>  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>引數  
 **'** *bind_token* **'**  
 語彙基元，可識別交易原先取得使用**sp_getbindtoken**或 Open Data Services **srv_getbindtoken**函式。 *bind_token*已**varchar(255)**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 繫結的兩個工作階段會共用交易和鎖定。 每個工作階段都會保留它自己的隔離等級，在一個工作階段上設定新的隔離等級，並不會影響另一工作階段的隔離等級。 每個工作階段都維持由它的安全性帳戶來識別，且只能存取帳戶已獲授權的資料庫資源。  
  
 **sp_bindsession**會使用繫結 token 繫結兩個或多個現有的用戶端工作階段。 這些用戶端工作階段必須在從中取得繫結 Token 的相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中。 工作階段是一個執行命令的用戶端。 繫結的資料庫工作階段會共用交易和鎖定空間。  
  
 從某個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體取得的繫結 Token，無法供連接到另一個執行個體的用戶端工作階段使用，即使是 DTC 交易也是如此。 繫結 Token 只在每個執行個體的本機環境內有效，不同的執行個體並不能共用它。 若要繫結上的另一個執行個體的用戶端工作階段[!INCLUDE[ssDE](../../includes/ssde-md.md)]，您必須執行，以取得不同的繫結語彙基元**sp_getbindtoken**。  
  
 **sp_bindsession**它會使用不在使用中的權杖，將會失敗並發生錯誤。  
  
 從使用工作階段解除繫結**sp_bindsession**而不指定*bind_token*或藉由傳遞中的 NULL *bind_token*。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將指定的繫結 Token 繫結到目前的工作階段。  
  
> [!NOTE]  
>  藉由執行取得繫結 token 範例所示**sp_getbindtoken**執行之前，先**sp_bindsession**。  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken&#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
