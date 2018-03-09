---
title: "建立密碼編譯提供者 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bedc5441c8119101a209de42358b38d20c288b8d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可延伸金鑰管理介面的 .dll 檔路徑。 當使用**SQL Server Connector for Microsoft Azure Key Vault**的預設位置是**' C:\Program Files\Microsoft SQL Server Connector for Microsoft Azure 金鑰 Vault\Microsoft.AzureKeyVaultService.EKM.dll'**.  
  
## <a name="remarks"></a>備註  
 提供者所建立的所有金鑰都會透過其 GUID 參考提供者。 GUID 會跨所有版本的 DLL 保留。  
  
 實作 SQLEKM 介面的 DLL 必須透過使用任何憑證的方式經過數位簽署。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會確認簽章。 這包括其憑證鏈結，必須將其根目錄安裝在**受信任的根憑證授權單位**Windows 系統上的位置。 如果簽章沒有經過正確驗證，CREATE CRYPTOGRAPHIC PROVIDER 陳述式會失敗。 如需有關憑證和憑證鏈結的詳細資訊，請參閱[SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
 當 EKM 提供者 dll 未實作所有必要的方法時，CREATE CRYPTOGRAPHIC PROVIDER 可以傳回錯誤 33085：  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 當用來建立 EKM 提供者 dll 的標頭檔過期時，CREATE CRYPTOGRAPHIC PROVIDER 可傳回錯誤 33032：  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限或成員資格**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會建立密碼編譯提供者，稱為`SecurityProvider`中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從.dll 檔案。 .Dll 檔案會命名為`c:\SecurityProvider\SecurityProvider_v1.dll`以及它是否已安裝在伺服器上。 您必須先將提供者的憑證安裝在伺服器上。  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>請參閱＜  
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
