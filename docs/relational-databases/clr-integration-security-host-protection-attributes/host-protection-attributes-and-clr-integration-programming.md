---
title: 通用語言執行時 (CLR) 主機保護屬性
description: CLR 提供了一種機制,用於在 .NET 框架中使用共享狀態、同步和外部進程Mgmt等屬性對託管 API 進行說明。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488047"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>主機保護屬性和 CLR 整合程式設計
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始，Common Language Runtime (CLR) 提供了一個機制來使用 CLR (如 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) 主機可能需要的某些屬性，為屬於 .NET Framework 之一部分的 Managed 應用程式開發介面 (API) 加註。 這類主機保護屬性 (HPA) 的範例包括：  
  
-   **共用狀態**,它指示 API 是否公開創建或管理共享狀態(例如,靜態類欄位)的能力。  
  
-   **同步**,指示 API 是否公開線上程之間執行同步的能力。  
  
-   **外部進程Mgmt**,它指示 API 是否公開控制主機進程的方法。  
  
 當提供了這些屬性時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指定 HPA 的清單，這些 HPA 是透過程式碼存取安全性 (CAS) 的主控環境內所不允許的。 CAS[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要求 由三個許可權集之一指定 **:SAFE、EXTERNAL_ACCESS**或**UNSAFE。** **EXTERNAL_ACCESS** 使用**CREATE ASSEMBLY**語句在伺服器上註冊程式集時,將指定這三個安全級別之一。 **在 SAFE**或**EXTERNAL_ACCESS**權限集中執行的代碼必須避免應用具有**System.Security.Security.Host 保護屬性**的某些類型或成員。 有關詳細資訊,請參閱[建立程式集](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)與[CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
 **Host保護屬性**與其說是提高可靠性的安全許可權,還因為它標識了主機可能不允許的特定代碼構造(類型或方法)。 使用 Host**保護屬性**強制執行一個程式設計模型,以幫助保護主機的穩定性。  
  
## <a name="host-protection-attributes"></a>主機保護屬性  
 HPA 可識別不適合主機程式設計模型以及代表下列可靠性威脅等級提高的類型或成員：  
  
-   否則為良性。  
  
-   可能會導致受伺服器管理的使用者程式碼不穩定。  
  
-   可能會導致伺服器處理序本身的不穩定。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不允許使用具有指定**系統.Security.Security.Security.Host 保護****屬性**的類型或成員,該類型或成員具有 **「外部行程Mgmt、****外部線程****、MayLeakOnAbort」、****安全基礎結構**、**自影響行程Mgmnt、****自影響線程**、**共用狀態**,**同步**或**UI**的值。 這會讓組件無法呼叫可啟用共用狀態、執行同步處理、在終止時可能造成資源流失，或是會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序完整性的成員。  
  
### <a name="disallowed-types-and-members"></a>不允許的類型和成員  
 以下主題標識其**主機保護資源**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值被 所不允許的類型和成員。  
  
> [!NOTE]  
>  這些主題中的清單是根據支援的組件產生的。  有關詳細資訊,請參閱支援的[.NET 框架庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
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
 [CLR 整合程式碼存取安全性](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合式程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [建立組件](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
