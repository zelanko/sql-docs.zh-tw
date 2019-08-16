---
title: sp_unregistercustomresolver & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3e84fb602c253f5ee6dd247c01bbbd64bda1d2f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017860"
---
# <a name="sp_unregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  取消登錄先前所登錄的商務邏輯模組。 商務邏輯可能採用 COM 元件或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件的形式。 這個預存程序是在登錄了自訂商務邏輯的散發者上執行的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>引數  
`[ @article_resolver = ] 'article_resolver'` 指定要取消登錄的自訂商務邏輯名稱。 *article_resolver*已**nvarchar(255)** ，沒有預設值。 如果移除的商務邏輯是 COM 元件，這個參數就是元件的易記名稱。 如果商務邏輯是一個 .NET Framework 組件，這個參數就是組件的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_unregistercustomresolver**用於合併式複寫中。  
  
 使用[sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)在複寫拓撲，拓撲返回已註冊的自訂商務邏輯模組或 COM 解析程式的清單中的任何伺服器上。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_unregistercustomresolver**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_lookupcustomresolver &#40;-SQL&AMP;&#41;&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;-SQL&AMP;&#41;&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
