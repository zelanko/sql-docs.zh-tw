---
title: CLR 整合代碼啟用安全性 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: f49968392dd813b48f43e5e63586fd0c6bec71d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118521"
---
# <a name="clr-integration-code-access-security"></a>CLR 整合程式碼存取安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) 支援稱為 Managed 程式碼之程式碼存取安全性的安全性模型。 在此模型中，將會根據程式碼的識別來授與權限給組件。 如需詳細資訊，請參閱 .NET Framework 軟體開發套件中的＜程式碼存取安全性＞一節。  
  
 下列三個不同的位置會定義可決定授與給組件之權限的安全性原則：  
  
-   電腦原則：此原則適用於在已安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之電腦中執行的所有 Managed 程式碼。  
  
-   使用者原則：此原則適用於由處理序主控的 Managed 程式碼。 若為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，則使用者原則為執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務之 Windows 帳戶所特有。  
  
-   主機原則：此原則由 CLR 的主機 (在此案例中為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 所設定，適用於在該主機中執行的 Managed 程式碼。  
  
 CLR 所支援的程式碼存取安全性機制是根據執行階段可以主控完全信任和部分信任程式碼的假設。 受 CLR 程式碼存取安全性保護的資源通常是由 Managed 應用程式開發介面所包裝，此介面在允許存取資源之前，會先要求對應的權限。 唯有在呼叫堆疊中所有的呼叫者 (在組件層級) 都具有對應的資源權限時，權限的要求才會被滿足。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內執行時授與給 Managed 程式碼的程式碼存取安全性權限集合是上述三個原則層級所授與之權限集合的交集。 即使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將權限集合授與給在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中載入的組件，使用者及電腦層級原則也會進一步限制指定給使用者程式碼的最終權限集合。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主機原則層級權限集合  
 由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則層級授與組件的程式碼存取安全性權限集合是由建立組件時指定的權限集合所決定。 有三個許可權集合： **SAFE**、 **EXTERNAL_ACCESS**和**UNSAFE** （使用[CREATE ASSEMBLY &#40;transact-sql&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)的**PERMISSION_SET**選項指定）。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在主控 CLR 時，會將主機層級的安全性原則層級提供給該 CLR；這項原則是在永遠會實行之兩個原則層級之下的另一個原則層級。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立的每一個應用程式網域都會設定此原則。 此原則不適用於當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立 CLR 執行個體時所生效的預設應用程式網域。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機層級原則，是系統組件的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固定原則，以及使用者組件的使用者指定原則的組合。  
  
 CLR 組件及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統組件的固定原則會授與它們完全的信任。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則之使用者指定的部分是根據指定每個組件之下列其中一個權限值區 (共三種) 的組件擁有者。 如需底下所列之安全性權限的詳細資訊，請參閱 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 僅允許內部計算和本機資料存取。 **SAFE**是限制最嚴格的許可權集合。 具有**安全**許可權之元件所執行的程式碼，無法存取外部系統資源，例如檔案、網路、環境變數或登錄。  
  
 **安全**元件具有下列許可權和值：  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|**SecurityPermission**|**執行：** 執行 managed 程式碼的許可權。|  
|**SqlClientPermission**|**內容連接 = true**，內容**連接 = 是**：只能使用內容連接，而且連接字串只能指定 "coNtext connection = true" 或 "coNtext connection = yes" 的值。<br /><br /> **AllowBlankPassword = false：** 不允許空白密碼。|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 元件具有與**安全**元件相同的許可權，而且能夠存取外部系統資源，例如檔案、網路、環境變數和登錄。  
  
 **EXTERNAL_ACCESS**元件也具有下列許可權和值：  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|不**受限制：** 允許分散式交易。|  
|**DNSPermission**|不**受限制：** 從功能變數名稱伺服器要求資訊的許可權。|  
|**EnvironmentPermission**|不**受限制：** 允許系統和使用者環境變數的完整存取權。|  
|**EventLogPermission**|**管理：** 允許採取下列動作：建立事件來源、讀取現有的記錄、刪除事件來源或記錄、回應專案、清除事件記錄檔、接聽事件，以及存取所有事件記錄檔的集合。|  
|**FileIOPermission**|不**受限制：** 允許對檔案和資料夾的完整存取。|  
|**KeyContainerPermission**|不**受限制：** 允許完整存取金鑰容器。|  
|**NetworkInformationPermission**|**存取：** 允許 ping。|  
|**RegistryPermission**|允許**HKEY_CLASSES_ROOT**、 **HKEY_LOCAL_MACHINE**、 **HKEY_CURRENT_USER**、 **HKEY_CURRENT_CONFIG**和 HKEY_USERS 的 [讀取] 許可權 **。**|  
|**SecurityPermission**|判斷提示 **：** 能夠判斷提示此程式碼的所有呼叫端都具有該作業的必要許可權。<br /><br /> **ControlPrincipal：** 操作主體物件的能力。<br /><br /> **執行：** 執行 managed 程式碼的許可權。<br /><br /> **SerializationFormatter：** 提供序列化服務的能力。|  
|**SmtpPermission**|**存取：** 允許對 SMTP 主機埠25的輸出連線。|  
|**SocketPermission**|**連接：** 允許傳輸位址上的輸出連接（所有埠、所有通訊協定）。|  
|**SqlClientPermission**|不**受限制：** 允許資料來源的完整存取權。|  
|**StorePermission**|不**受限制：** 允許 x.509 憑證存放區的完整存取權。|  
|**WebPermission**|**連接：** 允許對 web 資源的輸出連線。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 可讓組件無限制存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內外部的資源。 從**UNSAFE**元件內執行的程式碼也可以呼叫非受控碼。  
  
 **不安全**的元件會獲得**FullTrust**。  
  
> [!IMPORTANT]  
>  **** 對於執行計算和資料管理工作而不存取外部[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資源的元件而言，安全是建議的許可權設定。 **** 對於存取外部[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資源的元件，建議使用 EXTERNAL_ACCESS。 **EXTERNAL_ACCESS**元件預設會以[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務帳戶的身分執行。 **EXTERNAL_ACCESS**程式碼可以明確模擬呼叫者的 Windows 驗證安全性內容。 由於預設值是以[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務帳戶的身分執行，因此只能將執行**EXTERNAL_ACCESS**的許可權授與給以服務帳戶身分執行的登入。 從安全性的觀點來看， **EXTERNAL_ACCESS**和**UNSAFE**元件都相同。 不過， **EXTERNAL_ACCESS**元件提供各種可靠性和健全保護，而不是不**安全**元件。 指定**UNSAFE**可讓元件中的程式碼對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]進程空間執行不合法的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]作業，因此可能會危害的健全性和擴充性。 如需在中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立 clr 元件的詳細資訊，請參閱[管理 clr 整合元件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>存取外部資源  
 如果使用者定義型別（UDT）、預存程式或其他類型的結構元件都已向**安全**許可權集合註冊，則在結構中執行的受控碼就無法存取外部資源。 不過，如果指定了**EXTERNAL_ACCESS**或**UNSAFE**許可權集合，而 managed 程式碼嘗試存取外部資源， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]則會套用下列規則：  
  
|如果|對應行動|  
|--------|----------|  
|執行內容對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。|拒絕存取外部資源的嘗試，並引發安全性例外狀況。|  
|執行內容對應至 Windows 登入，並且執行內容是原始呼叫端。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容下存取外部資源。|  
|呼叫端不是原始呼叫端。|拒絕存取並引發安全性例外狀況。|  
|執行內容會對應至 Windows 登入、執行內容就是原始呼叫端，而且已模擬呼叫端。|存取會使用呼叫端安全性內容，而不是服務帳戶。|  
  
## <a name="permission-set-summary"></a>權限集合摘要  
 下圖摘要說明授與**SAFE**、 **EXTERNAL_ACCESS**和**UNSAFE**許可權集合的限制和許可權。  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**代碼啟用安全性許可權**|僅限 Execute|對外部資源的 Execute + 存取權|不受限制 (包括 P/Invoke)|  
|**程式設計模型限制**|是|是|無限制|  
|**可驗證性需求**|是|是|否|  
|**本機資料存取**|是|是|是|  
|**呼叫機器碼的能力**|否|否|是|  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [主機保護屬性和 CLR 整合程式設計](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 主控環境](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
