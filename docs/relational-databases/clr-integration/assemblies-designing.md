---
title: 設計組件 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 33519a8494be8f6a062227b81999f58c4f053071
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="assemblies---designing"></a>組件的設計
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述以下在設計組件時應該考慮的因數：  
  
-   封裝組件  
  
-   管理組件安全性  
  
-   組件的限制  
  
## <a name="packaging-assemblies"></a>封裝組件  
 組件在其類別及方法中，可以包含多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 常式或類型的功能。 大部分的情況下，封裝會在相同組件內執行相關函數的常式功能很有用處，尤其如果這些常式共用會彼此呼叫的類別。 例如，可為 Common Language Runtime (CLR) 觸發程序及 CLR 預存程序執行資料項目管理工作的類別，就可以封裝在相同的組件中。 這是因為這些類別的方法跟較不相關的那些工作相比，比較可能會彼此呼叫。  
  
 將程式碼封裝到組件時，應該要考慮以下事項：  
  
-   CLR 使用者定義型別及相依於 CLR 使用者自訂函數的索引，會導致保留的資料放在相依於組件的資料庫中。 資料庫中有相依於組件的保存資料時，修改組件的程式碼通常更為複雜。 因此，一般最好將保存資料相依性所依賴的程式碼 (例如，使用者定義型別及使用使用者自訂函數的索引)，跟沒有這類保存資料相依性的程式碼分開。 如需詳細資訊，請參閱[實作的組件](../../relational-databases/clr-integration/assemblies-implementing.md)和[ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
-   如果有段 Managed 程式碼需要更高的權限，最好將那個程式碼跟不需要較高權限的程式碼分隔，放在個別的組件。  
  
## <a name="managing-assembly-security"></a>管理組件安全性  
 您可以控制在執行 Managed 程式碼時，可存取受到「.NET 程式碼存取安全性」保護之資源的組件多寡。 建立或修改組件時，指定三種權限集之一，就可以完成此動作：SAFE、EXTERNAL_ACCESS 或 UNSAFE。  
  
### <a name="safe"></a>SAFE  
 SAFE 是預設的權限集，而且其限制最為嚴格。 由具有 SAFE 權限的組件執行的程式碼，無法存取外部系統資源，例如，檔案、網路、環境變數或登錄。 SAFE 程式碼可以存取本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料，或是執行不會存取本機資料庫以外資源的計算及商務邏輯。  
  
 執行計算及資料管理工作的大部分組件，不需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部的資源。 因此，建議您將 SAFE 作為組件權限集。  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 可讓組件存取特定的外部系統資源，例如，檔案、網路、Web 服務、環境變數及登錄。 只有當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以 EXTERNAL ACCESS 權限登入時，才能建立 EXTERNAL_ACCESS 組件。  
  
 SAFE 及 EXTERNAL_ACCESS 組件只能包含可驗證類型安全 (verifiably type-safe) 的程式碼。 這代表如果這些組件要存取類別，只能透過定義完善、對該類型定義有效的進入點。 因此，他們不能任意存取不屬於該程式碼的記憶體緩衝區。 此外，它們無法執行可能有損 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序強固性的作業。  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 可讓組件無限制存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內外部的資源。 由 UNSAFE 組件內執行的程式碼可以呼叫 Unmanaged 程式碼。  
  
 此外，指定 UNSAFE 可讓組件中的程式碼，執行 CLR 檢查器視為類型安全的作業。 這些作業可能會以未受控制的方式，存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序空間的記憶體緩衝區。 UNSAFE 組件也可能會破壞 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Common Language Runtime 的安全性系統。 UNSAFE 權限應只能由經驗豐富的開發人員或系統管理員，授與高度信任的組件。 只有成員**sysadmin**固定的伺服器角色可以建立 UNSAFE 組件。  
  
## <a name="restrictions-on-assemblies"></a>組件的限制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對組件中的 Managed 程式碼有特定限制，以確保能以可靠且可擴充的方式執行程式碼。 這代表不會允許在 SAFE 及 EXTERNAL_ACCESS 組件中，執行會危害伺服器強固性的特定作業。  
  
### <a name="disallowed-custom-attributes"></a>不允許的自訂屬性  
 不能以下列自訂屬性註解組件：  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 此外，不能以下列自訂屬性註解 SAFE 和 EXTERNAL_ACCESS 組件：  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>不允許的 .NET Framework API  
 任何[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]註解的其中一個，以不允許應用程式開發介面**HostProtectionAttributes**不能從 SAFE 和 EXTERNAL_ACCESS 組件呼叫。  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>支援的 .NET Framework 組件  
 您必須使用 CREATE ASSEMBLY，將自訂組件所參考的任何組件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 下列 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 組件已經載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因此不必使用 CREATE ASSEMBLY，就可以讓自訂組件參考這些組件。  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>另請參閱  
 [組件 & #40; Database engine& #41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [CLR 整合安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
