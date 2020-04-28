---
title: sp_bindsession （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: fac327d88aa8a6d74e153c1c7b2f3d637bf6f936
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68046020"
---
# <a name="sp_bindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將會話系結或解除系結至相同實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]中的其他會話。 繫結工作階段可讓兩個或更多工作階段參與相同的交易和共用鎖定，直到發出 ROLLBACK TRANSACTION 或 COMMIT TRANSACTION 為止。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用 Multiple Active Result Set (MARS) 或分散式交易。 如需詳細資訊，請參閱[使用 Multiple Active Result Sets &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>引數  
 **'** *bind_token* **'**  
 這是用來識別原本使用**sp_getbindtoken**或 Open 資料服務**srv_getbindtoken**函式所取得之交易的 token。 *bind_token*為**Varchar （255）**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 繫結的兩個工作階段會共用交易和鎖定。 每個工作階段都會保留它自己的隔離等級，在一個工作階段上設定新的隔離等級，並不會影響另一工作階段的隔離等級。 每個工作階段都維持由它的安全性帳戶來識別，且只能存取帳戶已獲授權的資料庫資源。  
  
 **sp_bindsession**會使用系結 token 來系結兩個或多個現有的用戶端會話。 這些用戶端工作階段必須在從中取得繫結 Token 的相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中。 工作階段是一個執行命令的用戶端。 繫結的資料庫工作階段會共用交易和鎖定空間。  
  
 從某個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體取得的繫結 Token，無法供連接到另一個執行個體的用戶端工作階段使用，即使是 DTC 交易也是如此。 繫結 Token 只在每個執行個體的本機環境內有效，不同的執行個體並不能共用它。 若要系結另一個實例上的[!INCLUDE[ssDE](../../includes/ssde-md.md)]用戶端會話，您必須藉由執行**sp_getbindtoken**來取得不同的系結 token。  
  
 如果**sp_bindsession**在使用非作用中的權杖時，將會失敗並產生錯誤。  
  
 藉由使用**sp_bindsession**而不指定*bind_token* ，或在*bind_token*中傳遞 Null，從會話解除系結。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將指定的繫結 Token 繫結到目前的工作階段。  
  
> [!NOTE]  
>  範例中所示的系結 token 是藉由在執行**sp_bindsession**之前執行**sp_getbindtoken**來取得。  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_getbindtoken &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;擴充預存程式 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
