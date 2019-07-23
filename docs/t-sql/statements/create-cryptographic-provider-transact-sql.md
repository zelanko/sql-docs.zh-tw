---
title: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d17e61de477b896a8fcdaead01d12674d3b9fddc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061025"
---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，建立可延伸金鑰管理 (Extensible Key Management，EKM) 提供者的密碼編譯提供者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  
  
## <a name="arguments"></a>引數  
 *provider_name*  
 「可延伸金鑰管理」提供者的名稱。  
  
 *path_of_DLL*  
 實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可延伸金鑰管理介面的 .dll 檔路徑。 使用**適用於 Microsoft Azure Key Vault 的 SQL Server 連接器**時，預設位置是 **'C:\Program Files\Microsoft SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll'** 。  
  
## <a name="remarks"></a>Remarks  
 提供者所建立的所有金鑰都會透過其 GUID 參考提供者。 GUID 會跨所有版本的 DLL 保留。  
  
 實作 SQLEKM 介面的 DLL 必須透過使用任何憑證的方式經過數位簽署。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會確認簽章。 這包括其憑證鏈結；該憑證鏈結的根目錄必須安裝在 Windows 系統的**受信任的根憑證授權單位**位置上。 如果簽章沒有經過正確驗證，CREATE CRYPTOGRAPHIC PROVIDER 陳述式將會失敗。 如需憑證和憑證鏈結的詳細資訊，請參閱 [SQL Server 憑證與非對稱金鑰](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
 當 EKM 提供者 dll 未實作所有必要的方法時，CREATE CRYPTOGRAPHIC PROVIDER 可以傳回錯誤 33085：  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 當用來建立 EKM 提供者 dll 的標頭檔過期時，CREATE CRYPTOGRAPHIC PROVIDER 可傳回錯誤 33032：  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>權限  
 需要 CONTROL SERVER 權限或 **sysadmin** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .dll 檔中，建立名稱為 `SecurityProvider` 的密碼編譯提供者。 .dll 檔案的名稱為 `c:\SecurityProvider\SecurityProvider_v1.dll`，並會安裝在伺服器上。 您必須先將提供者的憑證安裝在伺服器上。  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>另請參閱  
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
