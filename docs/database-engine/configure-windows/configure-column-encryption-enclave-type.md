---
title: 設定 Always Encrypted 伺服器設定選項的記憶體保護區類型 | Microsoft Docs
description: 了解如何啟用或停用 Always Encrypted 的安全記憶體保護區。 了解如何確認記憶體保護區是否已正確初始化。
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 39ad6bdc8911a0596d619f6d6a68de07d733dd6f
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279412"
---
# <a name="configure-the-enclave-type-for-always-encrypted-server-configuration-option"></a>設定 Always Encrypted 伺服器設定選項的記憶體保護區類型

[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本文描述如何針對具有安全記憶體保護區的 Always Encrypted 啟用或停用安全記憶體保護區。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

[資料行加密記憶體保護區類型] 伺服器設定選項可控制用於 Always Encrypted 的安全記憶體保護區類型。 可將此選項設定為下列其中一個值：  
  
|值|描述|  
|-------------------|-----------------| 
|0|**無安全記憶體保護區**。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將不會初始化 Always Encrypted 的安全記憶體保護區。 因此，將無法使用具有安全記憶體保護區之 Always Encrypted 的功能。|  
|1|**虛擬化型安全性 (VBS)** 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將嘗試初始化虛擬式安全性 (VBS) 記憶體保護區。

> [!IMPORTANT]
> 除非您重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，否則 [資料行加密記憶體保護區類型] 的變更不會生效。
   
您可以使用 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 檢視，檢查已設定記憶體保護區類型值和目前作用中的記憶體保護區類型值。 

若要確認在上次重新啟動 [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] 後已正確初始化目前作用中類型 (大於 0) 的記憶體保護區，請檢查 [sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md) 檢視：
 - 如果此檢視只包含一個資料列，則表示記憶體保護區已正確初始化。 
 - 如果此檢視未包含任何資料列，請檢查 SQL Server 錯誤記錄檔中是否有記憶體保護區初始化錯誤 - 請參閱[檢視 SQL Server 錯誤記錄檔 (SQL Server Management Studio)](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)。

如需如何設定 VBS 記憶體保護區的逐步指示，請參閱[在 SQL Server 中啟用具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md#step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server)。

## <a name="examples"></a>範例  
 下列範例會啟用安全記憶體保護區，並將記憶體保護區類型設定為 VBS：

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

下列查詢會擷取設定的記憶體保護區類型，以及目前作用中的記憶體保護區類型：

```sql  
USE [master];
GO
SELECT
[value]
, CASE [value] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_description]
, [value_in_use]
, CASE [value_in_use] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_in_use_description]
FROM sys.configurations
WHERE [name] = 'column encryption enclave type'; 
```  
## <a name="next-steps"></a>後續步驟
 [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md)   
