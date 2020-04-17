---
title: CLR 整合程式碼存取安全性 |微軟文件
description: 對於 SQL Server CLR 整合,CLR 支援託管代碼的代碼存取安全性,根據代碼標識向程式集授予許可權。
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
ms.openlocfilehash: 912db3acb6f6dc21952e99da31a1484a9745ed0b
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488305"
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
 由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則層級授與組件的程式碼存取安全性權限集合是由建立組件時指定的權限集合所決定。 有三個許可權集 **:SAFE、EXTERNAL_ACCESS**和**SAFE(** 使用["創建程式集&#40;交易-SQL&#41;)PERMISSION_SET](../../../t-sql/statements/create-assembly-transact-sql.md)選項指定)。 **EXTERNAL_ACCESS** **PERMISSION_SET**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在主控 CLR 時，會將主機層級的安全性原則層級提供給該 CLR；這項原則是在永遠會實行之兩個原則層級之下的另一個原則層級。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立的每一個應用程式網域都會設定此原則。 此原則不適用於當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立 CLR 執行個體時所生效的預設應用程式網域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機層級原則，是系統組件的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固定原則，以及使用者組件的使用者指定原則的組合。  
  
 CLR 組件及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統組件的固定原則會授與它們完全的信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機原則之使用者指定的部分是根據指定每個組件之下列其中一個權限值區 (共三種) 的組件擁有者。 如需底下所列之安全性權限的詳細資訊，請參閱 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 僅允許內部計算和本機資料存取。 **SAFE**是最嚴格的許可權集。 具有**SAFE**許可權的程式集執行的代碼無法存取外部系統資源,如檔、網路、環境變數或註冊表。  
  
 **SAFE**程式集具有以下權限和值:  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|**安全許可**|**執行:** 執行託管代碼的許可權。|  
|**SqlClientPermission**|**內容連接 : true,****上下文連線 = 是**:只能使用上下文連線,並且連接字串只能指定「上下文連接_true」或「上下文連線=是」的值。<br /><br /> **允許空白密碼 = 錯誤:** 不允許使用空白密碼。|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 程式集EXTERNAL_ACCESS具有與**SAFE**程式集相同的許可權,具有訪問外部系統資源(如檔、網路、環境變數和註冊表)的額外能力。  
  
 **EXTERNAL_ACCESS**程式集也具有以下權限和值:  
  
|權限|值/描述|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**未限制:** 允許分散式事務。|  
|**DNSPermission**|**未限制:** 從功能變數名稱伺服器請求信息的許可權。|  
|**EnvironmentPermission**|**未限制:** 允許完全訪問系統和用戶環境變數。|  
|**EventLogPermission**|**管理:** 允許以下操作:創建事件源、讀取現有日誌、刪除事件源或日誌、回應條目、清除事件日誌、偵聽事件以及訪問所有事件日誌的集合。|  
|**FileIOPermission**|**未限制:** 允許對文件和資料夾的完全訪問許可權。|  
|**KeyContainerPermission**|**未限制:** 允許完全訪問關鍵容器。|  
|**NetworkInformationPermission**|**存取:** 允許 Pinging。|  
|**RegistryPermission**|允許讀取HKEY_CLASSES_ROOT、HKEY_LOCAL_MACHINE、HKEY_CURRENT_USER、HKEY_CURRENT_CONFIG和**HKEY_CURRENT_CONFIG****HKEY_USERS的**讀取**HKEY_CLASSES_ROOT****HKEY_LOCAL_MACHINE****HKEY_CURRENT_USER**權。|  
|**安全許可**|**斷言:** 能夠斷言此代碼的所有調用方都具有操作的必要許可權。<br /><br /> **控制主體:** 能夠操作主體物件。<br /><br /> **執行:** 執行託管代碼的許可權。<br /><br /> **序列化 For物質:** 能夠提供序列化服務。|  
|**SmtpPermission**|**存取:** 允許與 SMTP 主機埠 25 的出站連接。|  
|**SocketPermission**|**連線:** 允許傳輸位址上的出站連接(所有埠、所有協定)。|  
|**SqlClientPermission**|**未限制:** 允許對數據源的完全訪問。|  
|**StorePermission**|**未限制:** 允許完全訪問 X.509 憑證儲存。|  
|**WebPermission**|**連線:** 允許與 Web 資源的出站連接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 可讓組件無限制存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內外部的資源。 在**UNSAFE**程式集中執行的代碼也可以調用非託管代碼。  
  
 **UNSAFE**程式集被給予**完全信任**。  
  
> [!IMPORTANT]  
>  **SAFE**是執行計算和數據管理任務的程式集的推薦許可權設置,而不訪問[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部的資源。 建議**對**訪問[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部資源的程式集EXTERNAL_ACCESS。 默認情況下**EXTERNAL_ACCESS**程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]集作為 服務帳戶執行。 **EXTERNAL_ACCESS**代碼可以顯式類比調用方的 Windows 身份驗證安全上下文。 由於預設值是作為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務帳戶執行,因此應僅授予受信任作為服務帳戶運行的登錄名執行**EXTERNAL_ACCESS**的許可權。 從安全角度來看 **,EXTERNAL_ACCESS**和**UNSAFE**程式集是相同的。 但是 **,EXTERNAL_ACCESS**元件提供了不在**UNSAFE**程式集中的各種可靠性和魯棒性保護。 指定**UNSAFE**允許程式集中的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]代碼對 進程空間執行非法操作,因此[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可能會危及的魯棒性和可伸縮性。 有關在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立 CLR 程式集的詳細資訊,請參考管理[CLR 整合程式集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>存取外部資源  
 如果使用者定義的類型 (UDT)、儲存過程或其他類型的建構程式集註冊到**SAFE**許可權集,則在構造中執行的託管代碼無法存取外部資源。 但是,如果指定**了EXTERNAL_ACCESS**或**UNSAFE**許可權集,並且託管代碼嘗試訪問外部資源[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)],請 應用以下規則:  
  
|If|結果為|  
|--------|----------|  
|執行內容對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。|拒絕存取外部資源的嘗試，並引發安全性例外狀況。|  
|執行內容對應至 Windows 登入，並且執行內容是原始呼叫端。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容下存取外部資源。|  
|呼叫端不是原始呼叫端。|拒絕存取並引發安全性例外狀況。|  
|執行內容會對應至 Windows 登入、執行內容就是原始呼叫端，而且已模擬呼叫端。|存取會使用呼叫端安全性內容，而不是服務帳戶。|  
  
## <a name="permission-set-summary"></a>權限集合摘要  
 下圖總結了授予**SAFE、EXTERNAL_ACCESS**和**UNSAFE**許可權集**EXTERNAL_ACCESS**的限制和許可權。  
  
|||||  
|-|-|-|-|  
||**安全**|**EXTERNAL_ACCESS**|**安全**|  
|**程式碼存取安全權限**|僅限 Execute|對外部資源的 Execute + 存取權|不受限制 (包括 P/Invoke)|  
|**程式設計模型限制**|是|是|無限制|  
|**可驗證性需求**|是|是|否|  
|**本地資料存取**|是|是|是|  
|**呼叫機器碼的能力**|否|否|是|  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [主機保護屬性和 CLR 整合程式設計](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 整合式程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 主控環境](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
