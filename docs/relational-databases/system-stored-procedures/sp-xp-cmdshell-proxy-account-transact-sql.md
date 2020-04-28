---
title: sp_xp_cmdshell_proxy_account （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xp_cmdshell_proxy_account
- sp_xp_cmdshell_proxy_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xp_cmdshell_proxy_account
- xp_cmdshell
ms.assetid: f807c373-7fbc-4108-a2bd-73b48a236003
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 59ea64e16f1469c12461a559c3f102094615fa12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67950465"
---
# <a name="sp_xp_cmdshell_proxy_account-transact-sql"></a>sp_xp_cmdshell_proxy_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立**xp_cmdshell**的 proxy 認證。  
  
> [!NOTE]  
>  預設會停用**xp_cmdshell** 。 若要啟用**xp_cmdshell**，請參閱[Xp_cmdshell 伺服器設定選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>引數  
 NULL  
 指定應該刪除 Proxy 認證。  
  
 *account_name*  
 指定將成為 Proxy 的 Windows 登入。  
  
 *password*  
 指定 Windows 帳戶的密碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 Proxy 認證將會被稱為 **# #xp_cmdshell_proxy_account # #**。  
  
 當使用 Null 選項執行時， **sp_xp_cmdshell_proxy_account**會刪除 proxy 認證。  
  
## <a name="permissions"></a>權限  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-the-proxy-credential"></a>A. 建立 Proxy 認證  
 下列範例會顯示如何針對一個稱為 `ADVWKS\Max04` 且具有密碼 `ds35efg##65` 的 Windows 帳戶建立 Proxy 認證。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'ADVWKS\Max04', 'ds35efg##65';  
GO  
```  
  
### <a name="b-dropping-the-proxy-credential"></a>B. 卸除 Proxy 認證  
 下列範例會從認證存放區移除 Proxy 認證。  
  
```  
EXEC sp_xp_cmdshell_proxy_account NULL;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [xp_cmdshell &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [&#40;Transact-sql&#41;建立認證](../../t-sql/statements/create-credential-transact-sql.md)   
 [&#40;Transact-sql&#41;的認證](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
