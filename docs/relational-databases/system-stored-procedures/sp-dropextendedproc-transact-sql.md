---
title: p (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 23361e6f28bdb87ab35a39ec68b448a60ad677d0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
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
 [  **@functname =**] **'***程序***'**  
 這是要卸除的擴充預存程序名稱。 *程序*是**nvarchar （517)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 執行**sp_dropextendedproc**卸除使用者定義擴充預存程序名稱，從[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目錄檢視和移除的項目從[sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目錄檢視。 這個預存程序可以僅在執行**主要**資料庫。  
  
**sp_dropextendedproc**不會卸除系統擴充預存程序。 相反地，系統管理員應該拒絕擴充預存程序的 EXECUTE 權限**公用**角色。  
  
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
 [sp_addextendedproc &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
