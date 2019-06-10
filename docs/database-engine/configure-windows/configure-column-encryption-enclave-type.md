---
title: 資料行加密記憶體保護區類型伺服器設定選項 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: jroth
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 1031bdfa3aa6c728d3e33b500fe942d5e52c5fdc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799464"
---
# <a name="column-encryption-enclave-type-server-configuration-option"></a>資料行加密記憶體保護區類型伺服器設定選項
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  使用**資料行加密記憶體保護區類型**選項，啟用或停用 Always Encrypted 的安全記憶體保護區。  如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

 下表列出可能的**資料行加密記憶體保護區類型**值：  
  
|ReplTest1|Description|  
|-------------------|-----------------|  
|0|**無安全記憶體保護區**。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將不會初始化 Always Encrypted 的安全記憶體保護區。 因此，將無法使用具有安全記憶體保護區之 Always Encrypted 的功能。|  
|1|**虛擬化型安全性 (VBS)** 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將會初始化 Always Encrypted 的安全記憶體保護區 (VBS 安全記憶體保護區)。|    

> [!IMPORTANT]
> 除非您重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，否則**資料行加密記憶體保護區類型**不會生效。
  
   
## <a name="examples"></a>範例  
 下列範例會啟用安全記憶體保護區：  

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

下列範例會停用安全記憶體保護區：  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
