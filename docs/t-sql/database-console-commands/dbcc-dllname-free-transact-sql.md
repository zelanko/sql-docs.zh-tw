---
title: DBCC dllname (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
author: pmasl
ms.author: umajay
ms.openlocfilehash: cc9716cbd1e27c6589b964c3c3d6208105f4863c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68101953"
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
可從記憶體卸載指定的擴充預存程序 DLL。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 \<*dllname*>  
 這是要從記憶體釋出的 DLL 名稱。  
  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註
在執行擴充預存程序時，DLL 仍由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體載入，直到伺服器關閉為止。 這個陳述式可讓 DLL 從記憶體卸載，而不必關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要顯示目前由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 載入的 DLL 檔，請執行 **sp_helpextendedproc**
  
## <a name="result-sets"></a>結果集  
當您指定有效的 DLL 之後，DBCC *dllname* (FREE) 會傳回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>權限  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
下列範例假設 `xp_sample` 是實作為 Xp_sample.dll，而且已經執行。 DBCC \<*dllname*> (FREE) 會卸載與 `xp_sample` 擴充程序相關的 xp_sample.dll 檔。
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[擴充預存程序的執行特性](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[卸載擴充預存程序 DLL](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
