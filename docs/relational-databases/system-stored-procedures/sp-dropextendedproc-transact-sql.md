---
title: sp_dropextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3690d4c954ae3cde5159100280597af14a796d3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529760"
---
# <a name="spdropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除擴充預存程序。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CLR 整合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>引數  
`[ @functname = ] 'procedure'` 是要卸除的擴充預存程序的名稱。 *程序*已**nvarchar(517)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 執行**sp_dropextendedproc**卸除使用者定義擴充預存程序名稱，從[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目錄檢視，並移除的項目[sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目錄檢視。 可以只在執行這個預存程序**主要**資料庫。  
  
**sp_dropextendedproc**未卸除系統擴充預存程序。 相反地，由系統管理員應該拒絕擴充預存程序的 EXECUTE 權限**公開**角色。  
  
 **sp_dropextendedproc**無法在交易內執行。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_dropextendedproc**。  
  
## <a name="examples"></a>範例  
 下列範例會卸除 `xp_hello` 擴充預存程序。  
  
> [!NOTE]  
>  這個擴充預存程序必須已經存在，否則該範例會傳回錯誤訊息。  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
