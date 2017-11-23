---
title: "sp_helpextendedproc (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c5ce565f6e393f09aa25c63fc8d12883434fb6d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告目前定義的擴充預存程序及程序 (函數) 所屬之動態連結程式庫 (DLL) 的名稱。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CLR 整合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@funcname =**] **'***程序***'**  
 這是報告的資訊所屬的擴充預存程序名稱。 *程序*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|擴充預存程序的名稱。|  
|**dll**|**nvarchar(255)**|DLL 的名稱。|  
  
## <a name="remarks"></a>備註  
 當*程序*指定，則**sp_helpextendedproc**報告指定擴充預存程序。 未提供這個參數時**sp_helpextendedproc**所屬的傳回所有擴充預存程序名稱，以及每個擴充預存程序的 DLL 名稱。  
  
## <a name="permissions"></a>Permissions  
 執行權限**sp_helpextendedproc**會授與**公用**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. 報告所有擴充預存程序的說明  
 下列範例會報告所有擴充預存程序。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. 報告單一擴充預存程序的說明  
 下列範例會報告`xp_cmdshell`擴充預存程序。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sp_addextendedproc &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
