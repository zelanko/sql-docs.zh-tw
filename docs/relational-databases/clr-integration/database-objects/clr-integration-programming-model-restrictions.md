---
title: CLR 整合式設計模型限制 |微軟文件
description: SQL Server 在首次使用 CREATE ASSEMBLY 和運行時註冊託管資料庫物件時執行代碼檢查。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: 83b73909cf1844796640a83910ee609eadd7dba4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488526"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 整合程式設計模型限制
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  構建託管存儲過程或其他託管資料庫物件時,需要考慮由[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]該物件執行某些代碼檢查。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]首次使用**CREATE ASSEMBLY**語句在資料庫中註冊託管代碼程式集時,在運行時執行檢查。 也會在執行階段檢查 Managed 程式碼，因為在組件中，可能會有執行階段絕對無法到達的程式碼路徑。  特別是這樣提供了註冊協力廠商組件的彈性，如此一來，當組件中的不安全程式碼設計為在用戶端環境中執行，但是絕對不會在主控的 CLR 內執行時，就不會封鎖該組件。 託管代碼必須滿足的要求取決於程式集是否註冊為**SAFE、EXTERNAL_ACCESS****SAFE**或**SAFE,****安全是**最嚴格的,下面列出。  
  
 除了對 Managed 程式碼組件所加諸的限制以外，也有授與的程式碼安全性權限。 Common Language Runtime (CLR) 支援稱為 Managed 程式碼之程式碼存取安全性 (CAS) 的安全性模型。 在此模型中，將會根據程式碼的識別來授與權限給組件。 **SAFE、EXTERNAL_ACCESS**和**UNSAFE**程式集具有不同的**EXTERNAL_ACCESS**CAS 許可權。 有關詳細資訊,請參閱[CLR 整合的程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY 檢查  
 運行**CREATE ASSEMBLY**語句時,將針對每個安全級別執行以下檢查。  如果任何檢查失敗,**建立程式集**將失敗,並出現錯誤訊息。  
  
### <a name="global-any-security-level"></a>全域 (任何安全性層級)  
 所有參考的組件都必須符合下列其中一個或多個準則：  
  
-   此組件已經在資料庫中註冊。  
  
-   此組件是其中一個支援的組件。 有關詳細資訊,請參閱支援的[.NET 框架庫](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
-   您正在使用 **「從**_\<位置>_ 建立程式集,並且所有參考的程式集及其依賴項目都可用於*\<位置>*。  
  
-   您使用的是 **「從**_\<位元組的建立」 >,_ 並且所有引用都透過分隔位元組的空間指定。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 所有**EXTERNAL_ACCESS**程式集必須符合以下條件:  
  
-   靜態欄位無法用來儲存資訊。 允許唯讀靜態欄位。  
  
-   通過 PEVerify 測試。 用來檢查 MSIL 程式碼及關聯的中繼資料確實符合類型安全需求的 PEVerify 工具 (peverify.exe) 隨附在 .NET Framework SDK 中。  
  
-   例如,不使用**同步屬性**類。  
  
-   不會使用 Finalizer 方法。  
  
 以下自訂屬性在**EXTERNAL_ACCESS**程式集中是不允許的:  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   檢查所有**EXTERNAL_ACCESS**裝配條件。  
  
## <a name="runtime-checks"></a>執行階段檢查  
 執行階段會檢查程式碼組件是否有下列條件。 如果找到這些條件的任何一個，將不允許執行 Managed 程式碼，而且將會擲回例外狀況。  
  
### <a name="unsafe"></a>UNSAFE  
 使用**System.反射.Assembly.Load()** 方法從位元組式顯示式載入程式集,或者透過反射隱式載入程式集 **。**  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 檢查所有**不安全**條件。  
  
 不允許在支援的組件清單中使用下列主機保護屬性 (HPA) 值當做註解的所有類型和方法。  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 有關 HPA 以及受支援的程式集中不允許的類型和成員的清單的詳細資訊,請參閱[主機保護屬性和 CLR 整合程式設計](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
### <a name="safe"></a>SAFE  
 檢查所有**EXTERNAL_ACCESS**條件。  
  
## <a name="see-also"></a>另請參閱  
 [支援的 .NET 架構庫](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [主機保護屬性和 CLR 整合程式設計](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
