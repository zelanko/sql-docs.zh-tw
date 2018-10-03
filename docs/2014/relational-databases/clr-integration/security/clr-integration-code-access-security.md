---
title: CLR 整合程式碼存取安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d829ef131bc8772ce2d84391513ffa52b2f2ff1a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075999"
---
# <a name="clr-integration-code-access-security"></a>CLR 整合程式碼存取安全性
  Common Language Runtime (CLR) 支援稱為 Managed 程式碼之程式碼存取安全性的安全性模型。 在此模型中，將會根據程式碼的識別來授與權限給組件。 如需詳細資訊，請參閱 .NET Framework 軟體開發套件中的＜程式碼存取安全性＞一節。  
  
 下列三個不同的位置會定義可決定授與給組件之權限的安全性原則：  
  
-   電腦原則：此原則適用於在已安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之電腦中執行的所有 Managed 程式碼。  
  
-   使用者原則：此原則適用於由處理序主控的 Managed 程式碼。 針對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務正在執行。  
  
-   主機原則：此原則由 CLR 的主機 (在此案例中為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 所設定，適用於在該主機中執行的 Managed 程式碼。  
  
 CLR 所支援的程式碼存取安全性機制是根據執行階段可以主控完全信任和部分信任程式碼的假設。 受 CLR 程式碼存取安全性的資源通常包裝由受管理的應用程式開發介面允許資源的存取權之前該 requirethe 對應權限。 只有當所有的呼叫端 （在組件層級） 的呼叫堆疊中具有對應的資源權限，會滿足 demandfor 權限。  
  
 程式碼存取安全性權限授與一組 managed 程式碼，在執行時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的權限集授與組件中載入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，授與使用者程式碼權限的最終集合可能會受到限制來進一步使用者及電腦層級原則。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主機原則層級權限集合  
 由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則層級授與組件的程式碼存取安全性權限集合是由建立組件時指定的權限集合所決定。 有三個權限集合： `SAFE`，`EXTERNAL_ACCESS`並`UNSAFE`(使用指定**PERMISSION_SET**選項[CREATE ASSEMBLY &#40;-&#41;](/sql/t-sql/statements/create-assembly-transact-sql)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 此原則不適用於當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立 CLR 執行個體時所生效的預設應用程式網域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Fixedpolicy 系統組件和使用者指定之原則的使用者組件。  
  
 CLR 組件及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統組件的固定原則會授與它們完全的信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則之使用者指定的部分是根據指定每個組件之下列其中一個權限值區 (共三種) 的組件擁有者。 如需底下所列之安全性權限的詳細資訊，請參閱 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 僅允許內部計算和本機資料存取。 `SAFE` 是限制最嚴格的權限集合。 具有 `SAFE` 權限之組件所執行的程式碼無法存取外部系統資源，例如檔案、網路、環境變數或登錄。  
  
 `SAFE` 組件具有下列權限和值：  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|`SecurityPermission`|`Execution:` 執行 Managed 程式碼的權限。|  
|`SqlClientPermission`|`Context connection = true`、`context connection = yes`：只能使用內容連接，而且連接字串只能指定 "context connection=true" 或 "context connection=yes" 的值。<br /><br /> **AllowBlankPassword = false:** 不允許空白密碼。|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 組件具有相同的權限`SAFE`組件，並附帶存取外部系統資源，例如檔案、 網路、 環境變數和登錄的能力。  
  
 `EXTERNAL_ACCESS` 組件也具有下列權限和值：  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:` 允許分散式的交易。|  
|`DNSPermission`|`Unrestricted:` 向網域名稱伺服器要求資訊的權限。|  
|`EnvironmentPermission`|`Unrestricted:` 允許對系統和使用者環境變數的完整存取。|  
|`EventLogPermission`|`Administer:` 允許下列動作：建立事件來源、讀取現有的記錄檔、刪除事件來源或記錄檔、回應項目、清除事件記錄檔、接聽事件及存取所有事件記錄檔的集合。|  
|`FileIOPermission`|`Unrestricted:` 允許對檔案和資料夾的完整存取。|  
|`KeyContainerPermission`|`Unrestricted:` 允許對金鑰容器的完整存取。|  
|`NetworkInformationPermission`|`Access:` 允許 Ping。|  
|`RegistryPermission`|允許對 `HKEY_CLASSES_ROOT`、`HKEY_LOCAL_MACHINE`、`HKEY_CURRENT_USER`、`HKEY_CURRENT_CONFIG` 和 `HKEY_USERS.` 的讀取權。|  
|`SecurityPermission`|`Assertion:` 判斷此程式碼的所有呼叫端都具有此作業之必要權限的功能。<br /><br /> `ControlPrincipal:` 操作主體物件的功能。<br /><br /> `Execution:` 執行 Managed 程式碼的權限。<br /><br /> `SerializationFormatter:` 提供序列化服務的功能。|  
|**SmtpPermission**|`Access:` 允許與 SMTP 主機通訊埠 25 的傳出連接。|  
|`SocketPermission`|`Connect:` 允許傳輸位址上的傳出連接 (所有通訊埠、所有通訊協定)。|  
|`SqlClientPermission`|`Unrestricted:` 允許對資料來源的完整存取。|  
|`StorePermission`|`Unrestricted:` 允許對 X.509 憑證存放區的完整存取。|  
|`WebPermission`|`Connect:` 允許對 Web 資源的傳出連接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 可讓組件無限制存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內外部的資源。 從 `UNSAFE` 組件內執行的程式碼也可以呼叫 Unmanaged 程式碼。  
  
 `UNSAFE` 會提供給 `FullTrust` 組件。  
  
> [!IMPORTANT]  
>  對於執行計算和資料管理工作而不存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外之資源的組件而言，`SAFE` 是建議的權限設定。 `EXTERNAL_ACCESS` 以執行組件預設[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務帳戶、 權限執行`EXTERNAL_ACCESS`只應該提供給受信任的服務帳戶身分執行的登入。 從安全性的角度來看，`EXTERNAL_ACCESS` 及 `UNSAFE` 組件相同。 不過，`EXTERNAL_ACCESS` 組件提供 `UNSAFE` 組件中沒有的各種可靠性及強固性保護。 指定`UNSAFE`允許執行不合法的作業，針對組件中的程式碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如需有關建立 CLR 組件中的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 管理 CLR 整合組件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>存取外部資源  
 如果使用者定義型別 (UDT)、預存程序或其他型別的建構組件是以 `SAFE` 權限集合註冊，在此建構中執行的 Managed 程式碼便無法存取外部資源。 不過，如果指定了 `EXTERNAL_ACCESS` 或 `UNSAFE` 權限集合，而 Managed 程式碼嘗試存取外部資源，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會套用下列規則：  
  
|如果|結果為|  
|--------|----------|  
|執行內容對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。|拒絕存取外部資源的嘗試，並引發安全性例外狀況。|  
|執行內容對應至 Windows 登入，並且執行內容是原始呼叫端。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容下存取外部資源。|  
|呼叫端不是原始呼叫端。|拒絕存取並引發安全性例外狀況。|  
|執行內容會對應至 Windows 登入、執行內容就是原始呼叫端，而且已模擬呼叫端。|存取會使用呼叫端安全性內容，而不是服務帳戶。|  
  
## <a name="permission-set-summary"></a>權限集合摘要  
 下圖將摘要列出授與 `SAFE`、`EXTERNAL_ACCESS` 和 `UNSAFE` 權限集合的權限與限制。  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|僅限 Execute|對外部資源的 Execute + 存取權|不受限制 (包括 P/Invoke)|  
|`Programming model restrictions`|是|是|無限制|  
|`Verifiability requirement`|是|是|否|  
|`Local data access`|是|是|是|  
|`Ability to call native code`|否|否|是|  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](clr-integration-security.md)   
 [主機保護屬性和 CLR 整合程式設計](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 主控環境](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
