---
title: CLR 託管環境 |Microsoft Docs
description: 本文說明如何整合 CLR 和 SQL Server，以一致的方式管理系統資源，以及如何整合 CAS 和 SQL Server 安全性。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
ms.openlocfilehash: 8824e427b71c26a8b6145db7cf60bbfc110e9ed5
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934372"
---
# <a name="clr-integration-architecture---clr-hosted-environment"></a>CLR 整合架構 - CLR 主控環境
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 .NET Framework Common Language Runtime (CLR) 整合可讓資料庫程式設計人員使用 Visual C#、Visual Basic .NET 和 Visual C++ 等語言。 程式設計人員可以使用這些語言所撰寫的商務邏輯種類包括函數、預存程序、觸發程序、資料類型和彙總。  
  
  CLR 會功能垃圾收集的記憶體、先占式執行緒、中繼資料服務 (類型反映) 、程式碼可驗證性和代碼啟用安全性。 CLR 會使用中繼資料來找出並載入類別、配置記憶體中的執行個體、解析方法引動過程、產生機器碼、強制使用安全性，和設定執行階段內容界限。  
  
 CLR 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行階段環境不同之處在於處理記憶體、執行緒與同步的方式。 本文描述這兩個執行時間的整合方式，以便一致地管理所有系統資源。 本文也涵蓋了 CLR 代碼啟用安全性 (CAS) 和安全性的整合方式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可為使用者程式碼提供可靠且安全的執行環境。  
  
## <a name="basic-concepts-of-clr-architecture"></a>CLR 架構的基本概念  
 在 .NET Framework 中，程式設計人員會以高階語言撰寫，實作定義其結構 (例如，類別的欄位或屬性) 和方法的類別。 這些方法中有部分可以是靜態函數。 編譯程式會產生一個稱為組件的檔案，其中包含利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 中繼語言 (MSIL) 編譯的程式碼，以及包含相依組件所有參考的資訊清單。  
  
> [!NOTE]  
>  組件是 CLR 架構中的重要元素。 它們是 .NET Framework 中，應用程式程式碼之封裝、部署與版本控制的單位。 您可以使用組件來部署資料庫內部的應用程式程式碼，並提供一個統一的方式來管理、備份與還原完整資料庫應用程式。  
  
 組件資訊清單包含組件的相關中繼資料，描述程式中定義的所有結構、欄位、屬性、類別、繼承關聯性、函數以及方法。 資訊清單會建立組件識別、指定組成組件實作的檔案、指定組成組件的類型和資源、列舉對其他組件的編譯時間相依性，並且指定組件正確執行所需的權限集合。 執行階段時會使用這個資訊來解析參考、強制執行版本繫結原則，以及驗證載入組件的完整性。  
  
 .NET Framework 支援註解類別、屬性 (Property)、函數和方法的自訂屬性 (Attribute)，以及應用程式可以在中繼資料中擷取的其他資訊。 所有 .NET Framework 編譯器都可以在不解譯的情況下使用這些註解，並將其當做組件中繼資料儲存。 這些註解可以使用與其他任何中繼資料相同的方式檢查。  
  
 Managed 程式碼是在 CLR 中以 MSIL 執行，而非直接由作業系統執行。 Managed 程式碼應用程式會取得自動記憶體回收、執行階段類型檢查和安全性支援等 CLR 服務。 這些服務會協助提供統一的 Managed 程式碼應用程式行為 (與平台和語言無關)。  
  
## <a name="design-goals-of-clr-integration"></a>CLR 整合的設計目標  
 當使用者程式碼在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (稱為 CLR 整合) 之 CLR 主控環境內部執行時，適用下列設計目標：  
  
###### <a name="reliability-safety"></a>可靠性 (安全性)  
 系統不允許使用者程式碼執行危害 Database Engine 程序完整性的作業，例如，彈出要求使用者回應或結束程序的訊息方塊。 使用者程式碼應該無法覆寫 Database Engine 記憶體緩衝區或內部資料結構。  
  
###### <a name="scalability"></a>延展性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 針對排程和記憶體管理，擁有不同的內部模型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在執行緒主動產生定期執行的情況下，或它們要等待鎖定或 I/O 時，支援合作式、非先佔式執行緒模型。 CLR 支援先佔式執行緒模型。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部執行的使用者程式碼可以直接呼叫作業系統執行緒原始物件，則它不會完整整合到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作排程器，而且可能會降低系統的延展性。 CLR 不會區別虛擬記憶體和實體記憶體，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會直接管理實體記憶體，而且需要在可設定的限制內使用實體記憶體。  
  
 用於執行緒、排序和記憶體管理的不同模型對於調整為支援數千個並行使用者工作階段的關聯式資料庫管理系統 (RDBMS) 會呈現整合性問題。 此架構應該確認針對執行緒、記憶體和同步處理原始物件直接呼叫應用程式開發介面 (API) 的使用者程式碼不會危害系統的延展性。  
  
###### <a name="security"></a>安全性  
 存取資料表或資料行之類的資料庫物件時，在資料庫中執行的使用者程式碼必須遵循 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證和授權規則。 此外，資料庫管理員應該能夠從資料庫中執行的使用者程式碼控制作業系統資源的存取權，例如檔案和網路存取權。 這種作法很重要，因為 managed 程式設計語言 (不同于非受控語言（例如 Transact-sql）) 會提供 Api 來存取這類資源。 系統必須為使用者程式碼提供一個安全的方式來存取 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序外部的電腦資源。 如需相關資訊，請參閱 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
###### <a name="performance"></a>效能  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中執行的 Managed 使用者程式碼應該擁有可與在伺服器外部執行之相同程式碼相比的計算效能。 從 Managed 使用者程式碼進行資料庫存取的速度不如原生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 快。 如需詳細資訊，請參閱[CLR 整合的效能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)。  
  
## <a name="clr-services"></a>CLR Services  
 CLR 提供數種服務協助達成 CLR 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 整合的設計目標。  
  
###### <a name="type-safety-verification"></a>類型安全性驗證  
 類型安全程式碼是只以妥善定義的方式存取記憶體結構的程式碼。 例如，在有一個有效的物件參考上，類型安全程式碼可以存取和實際欄位成員對應的固定位移上的記憶體。 然而，如果程式碼存取的記憶體，是位於該物件所屬記憶體範圍以內或以外的任意位移時，即不是類型安全。 當組件載入 CLR 時，在要使用 Just-In-Time (JIT) 編譯來編譯的 MSIL 前，執行階段會執行一個檢查程式碼來判斷其類型安全性的驗證階段。 成功通過此驗證的程式碼稱為可驗證類型安全 (verifiably type-safe) 的程式碼。  
  
###### <a name="application-domains"></a>應用程式網域  
 CLR 支援應用程式網域的概念，做為主機處理序內的執行區域，其中可以載入與執行 Managed 程式碼組件。 應用程式網域界限提供組件間的隔離。 組件會透過靜態變數與資料成員的可見性，以及動態呼叫程式碼的能力隔離。 應用程式網域也是載入和卸載程式碼的機制。 程式碼只能透過卸載應用程式網域來從記憶體卸載。 如需詳細資訊，請參閱[應用程式域和 CLR 整合安全性](https://docs.microsoft.com/previous-versions/sql/2014/database-engine/dev-guide/application-domains-and-clr-integration-security?view=sql-server-2014)。  
  
###### <a name="code-access-security-cas"></a>程式碼存取安全性 (CAS)  
 CLR 安全性系統提供一種方式來控制 Managed 程式碼可以透過指派權限給程式碼來執行的作業種類。 程式碼存取權限是根據程式碼識別指派的 (例如，組件的簽章或程式碼的來源)。  
  
 CLR 會提供電腦管理員可以設定的電腦通用原則。 此原則會針對在電腦上執行的任何 Managed 程式碼定義權限授權。 此外，在 Managed 程式碼上有一個主機 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 可以使用的主機層級安全性原則來指定額外的限制。  
  
 如果 .NET Framework 中的 Managed API 會公開受程式碼存取權限保護之資源的作業，則 API 將會在存取資源前要求權限。 此要求會使 CLR 安全性系統在呼叫堆疊中觸發每個程式碼單位 (組件) 的完整檢查。 只有在整個呼叫鏈具有許可權時，才會授與資源的存取權。  
  
 請注意，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 CLR 主控環境內部，不支援使用 Reflection.Emit API 動態產生 Managed 程式碼的功能。 此種程式碼將沒有要執行的 CAS 權限，因此會在執行階段失敗。 如需詳細資訊，請參閱[CLR 整合代碼啟用安全性](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
###### <a name="host-protection-attributes-hpas"></a>主機保護屬性 (HPA)  
 CLR 會提供一個機制來使用 CLR 主機可能需要的某些屬性，為屬於 .NET Framework 之一部分的 Managed API 加註。 這類屬性的範例包括：  
  
-   SharedState，它可指出 API 是否會公開建立或管理共用狀態 (如靜態類別欄位) 的功能。  
  
-   Synchronization，它可指出 API 是否會公開執行執行緒之間之同步處理的功能。  
  
-   ExternalProcessMgmt，它可指出 API 是否會公開控制主機處理序的方法。  
  
 當提供了這些屬性時，主機可以指定 HPA (如 SharedState 屬性) 的清單，在主控環境內應該不允許使用這些 HPA。 在此情況下，CLR 會拒絕使用者程式碼嘗試呼叫 HPA 在禁止清單中加註的 API。 如需詳細資訊，請參閱[主控制項保護屬性和 CLR 整合程式設計](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>SQL Server 和 CLR 如何一起運作  
 本節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何整合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 的執行緒、排程、同步處理以及記憶體管理模型。 特別是，本節會按照延展性、可靠性以及安全性目標來檢查整合效果。 當 CLR 裝載到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實質上會當做它的作業系統。 CLR 會針對執行緒、排程、同步處理與記憶體管理，呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所實作的低階常式。 這些常式與其余引擎所使用的基本類型相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 此方法提供數個延展性、可靠性與安全性優勢。  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>延展性：一般執行緒、排程與同步處理  
 CLR 會呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API 來建立執行緒，以便同時用於執行中的使用者程式碼和自己的內部用途。 若要在多個執行緒之間同步處理，CLR 會呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同步處理物件。 這種作法可讓排程器在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒等候同步處理物件時，排定其他工作。 例如，當 CLR 起始記憶體回收時，其所有執行緒都會等待記憶體回收完成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排程器知道它們所等待的 CLR 執行緒與同步處理物件，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以排程正在執行與 CLR 無關之其他資料庫工作的執行緒。 這也可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 偵測到包含 CLR 同步處理物件所採用之鎖定的死結，並採用傳統的技術來移除死結。  
  
 Managed 程式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中會以先佔式執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排程器可以偵測和停止需要大量時間產生的執行緒。 能夠將 CLR 執行緒攔截到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒意味著 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排程器可以在 CLR 中識別「失控的」執行緒，並管理其優先順序。 這種失控的執行緒會暫停，並放回到佇列中。 系統不允許重複識別為失控執行緒的執行緒在給定的期間內執行，讓其他執行中的工作者得以執行。  
  
 在某些情況下，長時間執行的 managed 程式碼會自動產生，而某些情況下則不會。 在下列情況下，長時間執行的 managed 程式碼將會自動產生：
 
 - 如果程式碼呼叫 SQL OS (來查詢資料，例如) 
 - 如果配置足夠的記憶體來觸發垃圾收集
 - 如果程式碼藉由呼叫 OS 函式進入搶先模式

 未執行上述任何作業的程式碼（例如僅包含計算的密封迴圈）不會自動產生排程器，這可能會導致系統中的其他工作負載等候時間過長。 在這些情況下，開發人員必須藉由呼叫 .NET Framework 的 Thread ( # A1 函式，或在預期長期執行的任何程式碼區段中，明確地進入 preemtive ( 模式，藉此明確地產生。 下列程式碼範例示範如何使用這些方法來手動產生。

 ```c#
// Example 1: Manually yield to SOS scheduler.
for (int i = 0; i < Int32.MaxValue; i++)
{
  // *Code that does compute-heavy operation, and does not call into
  // any OS functions.*

  // Manually yield to the scheduler regularly after every few cycles.
  if (i % 1000 == 0)
  {
    Thread.Sleep(0);
  }
}
 ```

```c#
// Example 2: Use ThreadAffinity to run preemptively.
// Within BeginThreadAffinity/EndThreadAffinity the CLR code runs in preemptive mode.
Thread.BeginThreadAffinity();
for (int i = 0; i < Int32.MaxValue; i++)
{
  // *Code that does compute-heavy operation, and does not call into
  // any OS functions.*
}
Thread.EndThreadAffinity();
```
  
###### <a name="scalability-common-memory-management"></a>延展性：一般記憶體管理  
 CLR 會呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原始物件來配置與取消配置其記憶體。 在系統的記憶體總使用量中包含 CLR 所使用的記憶體，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以維持在其設定的記憶體限制內，而且可以確保 CLR 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會爭用彼此的記憶體。 當系統記憶體受到限制時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以拒絕 CLR 記憶體要求，而且在其他工作需要記憶體時，可以要求 CLR 減少其記憶體的使用量。  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>可靠性：應用程式網域和無法復原的例外狀況  
 當 .NET Framework API 中的 Managed 程式碼遇到嚴重的例外狀況 (例如，記憶體不足或堆疊溢位) 時，不一定能夠從這類的失敗復原，也不一定能夠確保其實作的一致且正確的語意。 這些 API 會引發執行緒中止的例外狀況來回應這些失敗。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中主控時，此類執行緒中止的處理方式如下：CLR 會在執行緒中止發生所在的應用程式網域中偵測任何共用狀態。 CLR 會藉由檢查同步處理物件是否存在來偵測此情況。 如果在應用程式網域中有共用狀態，則會卸載應用程式網域本身。 卸載應用程式網域時，會停止目前正在該應用程式網域中執行的資料庫交易。 因為共用狀態的存在可能會擴大此類嚴重例外狀況對於使用者工作階段的影響，而非觸發例外狀況的影響，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 已經採取步驟來降低共用狀態的可能性。 如需詳細資訊，請參閱 .NET Framework 文件集。  
  
###### <a name="security-permission-sets"></a>安全性：權限集合  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可讓使用者針對資料庫中部署的程式碼指定可靠性和安全性需求。 將元件上傳至資料庫時，元件的作者可以為該元件指定三個許可權集合的其中一個： SAFE、EXTERNAL_ACCESS 和 UNSAFE。  
  
|功能|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|-|-|-|-|  
|程式碼存取安全性|僅限 Execute|對外部資源的 Execute + 存取權|不受限制|  
|程式設計模型限制|是|是|沒有限制|  
|可驗證性需求|是|是|否|  
|呼叫機器碼的能力|否|否|是|  
  
 SAFE 是最可靠及安全的模式，其包含了根據允許的程式設計模型的相關限制。 SAFE 組件有被授與足夠的權限來執行、進行運算，以及存取本機資料庫。 SAFE 組件需要是可驗證的類型安全，且不允許呼叫 Unmanaged 程式碼。  
  
 UNSAFE 適用於高度信任的程式碼，這類程式碼只能由資料庫管理員建立； 此信任的程式碼沒有程式碼存取安全性的限制，且可以呼叫 Unmanaged 程式碼 (機器碼)。  
  
 EXTERNAL_ACCESS 提供了中級安全性選項，可讓程式碼存取在資料庫外部的資源，但是仍然保有 SAFE 的可靠性保證。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用主機層級的 CAS 原則層來設定主機原則，以根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄中所儲存的權限集合來授與三個權限集合當中的一個。 在資料庫內執行的 Managed 程式碼一定會取得這些程式碼存取權限集合當中的一個。  
  
### <a name="programming-model-restrictions"></a>程式設計模型限制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 Managed 程式碼的程式設計模型包含撰寫函數、程序和類型，而這些項目通常不需要使用跨多個引動過程之間所保有的狀態或是共用跨多個使用者工作階段的狀態。 再者，如之前所述，共用狀態的存在可能會造成嚴重的例外狀況，而這些例外狀況會影響應用程式的延展性和可靠性。  
  
 基於這些考量，我們不鼓勵使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所使用之類別的靜態變數和靜態資料成員。 對於 SAFE 和 EXTERNAL_ACCESS 組件而言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在 CREATE ASSEMBLY 時檢查組件的中繼資料；如果發現有使用靜態資料成員和變數，則會讓這類組件的建立作業失敗。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也不允許呼叫以**SharedState**、**同步**處理和**ExternalProcessMgmt**主機保護屬性標注的 .NET Framework api。 這會讓 SAFE 和 EXTERNAL_ACCESS 組件無法呼叫可啟用共用狀態、執行同步處理，以及影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序完整性的任何 API。 如需詳細資訊，請參閱[CLR 整合程式設計模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 整合的效能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
