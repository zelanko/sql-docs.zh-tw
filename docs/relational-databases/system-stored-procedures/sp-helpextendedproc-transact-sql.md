---
title: sp_helpextendedproc （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8341f752b266d245603f849325dc32f90f9d92c2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828907"
---
# <a name="sp_helpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告目前定義的擴充預存程序及程序 (函數) 所屬之動態連結程式庫 (DLL) 的名稱。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[CLR 整合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @funcname = ] 'procedure'`這是報告的資訊所屬的擴充預存程式名稱。 程式是**sysname**，預設*值是 Null* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|擴充預存程序的名稱。|  
|**dll**|**nvarchar(255)**|DLL 的名稱。|  
  
## <a name="remarks"></a>備註  
 當指定了*procedure*時， **sp_helpextendedproc**會報告指定的擴充預存程式。 未提供此參數時， **sp_helpextendedproc**會傳回所有擴充預存程式名稱，以及每個擴充預存程式所屬的 DLL 名稱。  
  
## <a name="permissions"></a>權限  
 執行**sp_helpextendedproc**的許可權會授與**public**。  
  
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
 下列範例會報告 `xp_cmdshell` 擴充預存程式。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
