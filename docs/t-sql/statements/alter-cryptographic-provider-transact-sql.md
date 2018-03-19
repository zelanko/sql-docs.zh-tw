---
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL
- ALTER CRYPTOGRAPHIC PROVIDER
- ALTER_CRYPTOGRAPHIC_TSQL
- ALTER CRYPTOGRAPHIC
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER CRYPTOGRAPHIC PROVIDER
ms.assetid: 876b6348-fb29-49e1-befc-4217979f6416
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe377a27978cdae372a7bfc8545d7cad1f514820
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，改變 Extensible Key Management (EKM) 提供者的密碼編譯提供者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  
## <a name="arguments"></a>引數  
 *provider_name*  
 Extensible Key Management 提供者的名稱。  
  
 *Path_of_DLL*  
 實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extensible Key Management 介面之 .dll 檔的路徑。  
  
 ENABLE | DISABLE  
 啟用或停用提供者。  
  
## <a name="remarks"></a>Remarks  
 如果提供者變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用來實作 Extensible Key Management 的 .dll 檔案，您必須使用 ALTER CRYPTOGRAPHIC PROVIDER 陳述式。  
  
 當使用 ALTER CRYPTOGRAPHIC PROVIDER 陳述式來更新 .dll 檔案路徑時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行以下動作：  
-   停用此提供者。  
-   驗證 DLL 簽章，並確認此 .dll 檔案的 GUID 與目錄中記錄的 GUID 相同。  
-   更新此目錄中的 DLL 版本。  
  

當 EKM 提供者設定為 DISABLE 時，任何嘗試透過新連接搭配加密陳述式來使用此提供者的動作都將會失敗。  
  
若要停用提供者，使用此提供者的所有工作階段都必須結束。  
  
當 EKM 提供者 dll 未實作所有必要的方法時，ALTER CRYPTOGRAPHIC PROVIDER 可以傳回錯誤 33085：  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
當用來建立 EKM 提供者 dll 的標頭檔過期時，ALTER CRYPTOGRAPHIC PROVIDER 可傳回錯誤 33032：  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 需要密碼編譯提供者的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，將稱為 `SecurityProvider` 的密碼編譯提供者更改為更新版的 .dll 檔案。 這個新的版本命名為 `c:\SecurityProvider\SecurityProvider_v2.dll`，而且會安裝在伺服器上。 您必須將提供者的憑證安裝在伺服器上。  
  
1. 停用提供者以執行升級。 這將會終止所有開啟的密碼編譯工作階段。  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. 升級提供者 .dll 檔案。 GUID 必須與先前版本相同，但版本可以不同。  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. 啟用升級後的提供者。   
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
