---
title: 主機保護屬性和 CLR 整合程式設計 |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd3b430f3556eba9d6f9b510aa813bec2a6c9ad3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>主機保護屬性和 CLR 整合程式設計
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始，Common Language Runtime (CLR) 提供了一個機制來使用 CLR (如 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) 主機可能需要的某些屬性，為屬於 .NET Framework 之一部分的 Managed 應用程式開發介面 (API) 加註。 這類主機保護屬性 (HPA) 的範例包括：  
  
-   **SharedState**，指出 API 是否會公開能夠建立或管理共用狀態 （例如，靜態類別欄位）。  
  
-   **同步處理**，指出 API 是否會公開執行執行緒之間的同步處理的能力。  
  
-   **ExternalProcessMgmt**，指出 API 是否會公開控制主機處理序的方式。  
  
 當提供了這些屬性時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指定 HPA 的清單，這些 HPA 是透過程式碼存取安全性 (CAS) 的主控環境內所不允許的。 CAS 需求所指定的其中三個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用權限集合：**安全**， **EXTERNAL_ACCESS**，或**UNSAFE**。 三個安全性層級的其中一個指定的伺服器上，註冊組件時使用**CREATE ASSEMBLY**陳述式。 程式碼執行內**安全**或**EXTERNAL_ACCESS**使用權限集合必須避免特定類型或成員具有**System.Security.Permissions.HostProtectionAttribute**套用的屬性。 如需詳細資訊，請參閱[建立組件](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)和[CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
 **HostProtectionAttribute**不是安全性權限如往常般來改善可靠性，它會識別特定的程式碼建構，類型或方法時，主機可能不允許。 使用**HostProtectionAttribute**強制使用有助於保護主機的穩定性的程式設計模型。  
  
## <a name="host-protection-attributes"></a>主機保護屬性  
 HPA 可識別不適合主機程式設計模型以及代表下列可靠性威脅等級提高的類型或成員：  
  
-   否則為良性。  
  
-   可能會導致受伺服器管理的使用者程式碼不穩定。  
  
-   可能會導致伺服器處理序本身的不穩定。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許使用型別或成員具有**HostProtectionAttribute**指定**System.Security.Permissions.HostProtectionResource**列舉值是**ExternalProcessMgmt**， **ExternalThreading**， **MayLeakOnAbort**， **SecurityInfrastructure**， **SelfAffectingProcessMgmnt**， **SelfAffectingThreading**， **SharedState**，**同步**，或**UI**. 這會讓組件無法呼叫可啟用共用狀態、執行同步處理、在終止時可能造成資源流失，或是會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序完整性的成員。  
  
### <a name="disallowed-types-and-members"></a>不允許的類型和成員  
 下列主題將識別型別和成員的**HostProtectionResource**值不允許由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  這些主題中的清單是根據支援的組件產生的。  如需詳細資訊，請參閱[支援.NET Framework 程式庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [Microsoft.VisualBasic.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 列出 Microsoft.VisualBasic.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [Mscorlib.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 列出 mscorlib.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [System.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 列出 System.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [System.Data.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 列出 System.Data.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [System.Core.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 列出 System.Core.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合程式碼存取安全性](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [建立組件](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
