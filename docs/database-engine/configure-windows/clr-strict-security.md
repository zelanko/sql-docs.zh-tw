---
title: CLR 嚴格安全性 | Microsoft Docs
description: 如何設定 SQL Server 中的 CLR 嚴格安全性
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- clr strict security
- clr_strict_security_TSQL
- clr strict security
- strict_security_TSQL
helpviewer_keywords:
- assemblies [CLR integration], strick security
- clr strict security option
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7024f4214388f77edc2f97e402db8da71e9c857c
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205254"
---
# <a name="clr-strict-security"></a>CLR 嚴格安全性   
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 `SAFE`、`EXTERNAL ACCESS`、`UNSAFE` 權限的解譯。   

|ReplTest1 |Description | 
|----- |----- | 
|0 |Disabled - 針對回溯相容性所提供。 不建議使用 `Disabled` 值。 | 
|1 |Enabled - 讓 [!INCLUDE[ssde-md](../../includes/ssde-md.md)] 忽略組件的 `PERMISSION_SET` 資訊，而且一律會將它們解釋為 `UNSAFE`。  `Enabled` 是 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 的預設值。 | 

> [!WARNING]
>  CLR 使用 .NET Framework 中的程式碼存取安全性 (CAS)，而這不再支援為安全性界限。 使用 `PERMISSION_SET = SAFE` 所建立的 CLR 組件可以存取外部系統資源、呼叫 Unmanaged 程式碼，以及取得系統管理員權限。 從 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 開始，引進稱為 `clr strict security` 的 `sp_configure` 選項，來增強 CLR 組件的安全性。 `clr strict security` 會依預設啟用，且將 `SAFE` 與 `EXTERNAL_ACCESS` 組件視作已標記為 `UNSAFE` 一樣。 可以基於回溯相容性停用 `clr strict security` 選項，但不建議這麼做。 Microsoft 建議透過具有已獲授與 master 資料庫中 `UNSAFE ASSEMBLY` 權限之對應登入的憑證或非對稱金鑰簽署所有組件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員也可以將組件新增至資料庫引擎應該信任的組件清單。 如需詳細資訊，請參閱 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)。

## <a name="remarks"></a>Remarks   

啟用時，會在執行階段忽略 `CREATE ASSEMBLY` 和 `ALTER ASSEMBLY` 陳述式中的 `PERMISSION_SET` 選項，但在中繼資料中會保留 `PERMISSION_SET` 選項。 忽略此選項可將中斷現有程式碼陳述式最小化。

`CLR strict security` 是 `advanced option`。  

> [!IMPORTANT]
>  啟用嚴格安全性之後，將無法載入任何未簽署的組件。 您必須改變或置放並重新建立每個組件，以使用憑證或非對稱金鑰進行簽署，該金鑰有具有伺服器 `UNSAFE ASSEMBLY` 權限的對應登入。

## <a name="permissions"></a>[權限] 

### <a name="to-change-this-option"></a>變更此選項  
需要 `CONTROL SERVER` 權限或系統管理員 `sysadmin` 固定伺服器角色中的成員資格。

### <a name="to-create-an-clr-assembly"></a>建立 CLR 組件   
啟用 `CLR strict security` 時，需要有下列權限才能建立 CLR 組件：

- 使用者必須具有 `CREATE ASSEMBLY` 權限  
- 而且，下列其中一個條件也必須成立：  
  - 組件是使用憑證或非對稱金鑰進行簽署，該金鑰有具有伺服器 `UNSAFE ASSEMBLY` 權限的對應登入。 建議簽署組件。  
  - 資料庫的 `TRUSTWORTHY` 屬性設定為 `ON`，而且具有伺服器之 `UNSAFE ASSEMBLY` 權限的登入擁有資料庫。 不建議使用此選項。  

  
## <a name="see-also"></a>另請參閱  
  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CLR 已啟用伺服器組態選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)
