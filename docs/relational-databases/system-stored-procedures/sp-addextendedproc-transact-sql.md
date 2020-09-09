---
description: sp_addextendedproc (Transact-SQL)
title: sp_addextendedproc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e8c7ffebae9f082a6a579a6cb6643ad2fc44d1b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548385"
---
# <a name="sp_addextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  註冊新擴充預存程式的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CLR 整合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>引數  
`[ @functname = ] 'procedure'` 這是要在動態連結程式庫 (DLL) 中呼叫的函式名稱。 程式是**Nvarchar (517) ** *，沒有預設*值。 程式*可選擇性地*在表單*owner. function*中包含擁有者名稱。  
  
`[ @dllname = ] 'dll'` 這是包含函數的 DLL 名稱。 *dll* 是 **Varchar (255) **，沒有預設值。 建議您指定 DLL 的完整路徑。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 建立擴充預存程式之後，必須使用 sp_addextendedproc 將其加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **sp_addextendedproc** 如需詳細資訊，請參閱 [將擴充預存程式加入至 SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)。  
  
 此程式只能在 **master** 資料庫中執行。 若要從 **master**以外的資料庫執行擴充預存程式，請使用 **master**來限定擴充預存程式的名稱。  
  
 **sp_addextendedproc** 將專案加入至 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 目錄檢視，使用註冊新擴充預存程式的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 它也會在 [sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 目錄檢視中加入專案。  
  
> [!IMPORTANT]  
>  在升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，沒有用完整路徑來登錄的現有 DLL 無法運作。 若要修正此問題，請使用 **sp_dropextendedproc** 取消註冊 DLL，然後使用 **sp_addextendedproc**重新註冊，指定完整的路徑。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_addextendedproc**。  
  
## <a name="examples"></a>範例  
 下列範例會加入 **xp_hello** 擴充預存程式。  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>另請參閱  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
