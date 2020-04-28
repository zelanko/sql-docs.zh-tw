---
title: Common Language Runtime （CLR）主機保護屬性
description: CLR 提供一種機制，可使用 SharedState、同步處理和 ExternalProcessMgmt 等屬性來標注 .NET Framework 中受管理的 Api。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
ms.openlocfilehash: 2aeaeb5d4eb06d6d632a59300225d01cc4376369
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488047"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>主機保護屬性和 CLR 整合程式設計
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始，Common Language Runtime (CLR) 提供了一個機制來使用 CLR (如 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) 主機可能需要的某些屬性，為屬於 .NET Framework 之一部分的 Managed 應用程式開發介面 (API) 加註。 這類主機保護屬性 (HPA) 的範例包括：  
  
-   **SharedState**，它會指出 API 是否會公開建立或管理共用狀態的功能（例如，靜態類別欄位）。  
  
-   **同步**處理，指出 API 是否會公開執行執行緒之間同步處理的功能。  
  
-   **ExternalProcessMgmt**，指出 API 是否公開控制主機進程的方法。  
  
 當提供了這些屬性時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指定 HPA 的清單，這些 HPA 是透過程式碼存取安全性 (CAS) 的主控環境內所不允許的。 CA 需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是由三個許可權集合的其中一個所指定： **SAFE**、 **EXTERNAL_ACCESS**或**UNSAFE**。 當元件在伺服器上註冊時，會使用**CREATE assembly**語句來指定這三個安全性層級的其中一個。 在**SAFE**或**EXTERNAL_ACCESS**許可權集合內執行的程式碼，必須避免已套用**HostProtectionAttribute**屬性的特定類型或成員。 如需詳細資訊，請參閱[建立元件](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)和[CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
 **HostProtectionAttribute**並不是提升可靠性的安全性許可權，因為它會識別主機可能不允許的特定程式碼結構，也就是類型或方法。 使用**HostProtectionAttribute**會強制執行程式設計模型，以協助保護主機的穩定性。  
  
## <a name="host-protection-attributes"></a>主機保護屬性  
 HPA 可識別不適合主機程式設計模型以及代表下列可靠性威脅等級提高的類型或成員：  
  
-   否則為良性。  
  
-   可能會導致受伺服器管理的使用者程式碼不穩定。  
  
-   可能會導致伺服器處理序本身的不穩定。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不允許使用具有**HostProtectionAttribute**的類型或成員，其指定的**HostProtectionResource**列舉值為**ExternalProcessMgmt**、 **ExternalThreading**、 **MayLeakOnAbort**、 **SecurityInfrastructure**、 **SelfAffectingProcessMgmnt**、 **SelfAffectingThreading**、 **SharedState**、**同步**處理或**UI**。 這會讓組件無法呼叫可啟用共用狀態、執行同步處理、在終止時可能造成資源流失，或是會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序完整性的成員。  
  
### <a name="disallowed-types-and-members"></a>不允許的類型和成員  
 下列主題會識別不允許其**HostProtectionResource**值的類型和成員[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  這些主題中的清單是根據支援的組件產生的。  如需詳細資訊，請參閱[支援的 .NET Framework 程式庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [Microsoft.VisualBasic.dll 中不允許的型別和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 列出 Microsoft.VisualBasic.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [在 mscorlib.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 列出 mscorlib.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [在 System.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 列出 System.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [在 System.Data.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 列出 System.Data.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
 [System.Core.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 列出 System.Core.dll 中的一些類型和成員，這些類型和成員的 HPA 值是不被允許的。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合代碼啟用安全性](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [建立組件](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
