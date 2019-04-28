---
title: 多維度模型組件管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], assemblies
- calling user-defined functions
- user impersonation [Analysis Services]
- impersonation [Analysis Services]
- Data Mining Extensions [Analysis Services], assemblies
- MDX [Analysis Services], assemblies
- user-defined functions [Analysis Services]
- Analysis Services objects, assemblies
- assemblies [Analysis Services]
- application domains [Analysis Services]
ms.assetid: b2645d10-6d17-444e-9289-f111ec48bbfb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f5109e604c65d8a525e5c65127ca287c8e3b049
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725242"
---
# <a name="multidimensional-model-assemblies-management"></a>多維度模型組件管理
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供許多可與多維度運算式 (MDX) 和資料採礦延伸模組 (DMX) 語言搭配使用的內建函數，其設計目的是要完成從標準統計計算一直到階層中周遊成員間的各種運算。 但是，就如同其他複雜且強固的產品一樣，總是有進一步擴充產品功能的需求。  
  
 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可讓您將組件加入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或資料庫中。 組件可讓您使用任何 Common Language Runtime (CLR) 語言 (例如 Microsoft Visual Basic .NET 或 Microsoft Visual C#) 來建立外部使用者自訂函數。 您也可以使用元件物件模型 (COM) 自動化語言 (例如 Microsoft Visual Basic 或 Microsoft Visual C++)。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
 組件可以讓您延伸 MDX 和 DMX 的商務功能。 您可以將想要的功能建立成程式庫 (例如動態連結程式庫 (DLL))，然後將該程式庫當成組件加入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。 程式庫中的公用方法便公開給 MDX 和 DMX 運算式、程序、計算、動作，以及用戶端應用程式，作為使用者自訂函數。  
  
 具有新程序和函數的組件可加入到伺服器。 您可以使用組件來增強或加入伺服器未提供的自訂功能。 藉由使用組件，便可以將新的功能加入多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 或預存程序。 組件會從自訂應用程式執行所在的位置載入，而且會將組件二進位檔案的複本連同資料庫資料儲存在伺服器中。 當移除組件時，複製的組件也會從伺服器中移除。  
  
 組件可以有兩種不同類型：COM 和 CLR。 CLR 組件是使用 .NET Framework 程式設計語言 (如 C#、Visual Basic .NET、Managed C++) 開發的組件。 COM 組件是必須在伺服器上註冊的 COM 程式庫。  
  
 組件可加入 <xref:Microsoft.AnalysisServices.Server> 或 <xref:Microsoft.AnalysisServices.Database> 物件。 伺服器組件可由連接到伺服器或伺服器中任何物件的任何使用者所呼叫。 資料庫組件只能由連接到資料庫的 <xref:Microsoft.AnalysisServices.Database> 物件或使用者所呼叫。  
  
 簡單 <xref:Microsoft.AnalysisServices.Assembly> 物件是由基本資訊 (名稱和識別碼)、檔案集合和安全性規格所組成。  
  
 檔案集合指的是載入的組件檔案以及其對應的偵錯 (.pdb) 檔案 (如果這些偵錯檔案與組件檔案一起載入)。 組件檔案會從應用程式定義檔案的位置載入，而且會將複本連同資料儲存在伺服器中。 組件檔案的複本是用在每次啟動服務時載入組件。  
  
 安全性指定包含用來執行組件的權限集合和模擬。  
  
## <a name="calling-user-defined-functions"></a>呼叫使用者定義函數  
 在組件中呼叫使用者自訂函數的方式，與呼叫內建函數的方式相同，只不過您需要使用完整名稱。 例如，傳回 MDX 所預期類型的使用者自訂函數，會包含在 MDX 查詢中，如下列範例所示：  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 使用者自訂函數亦可使用 CALL 關鍵字呼叫。 針對會傳回資料錄集或空值的使用者自訂函數，您必須使用 CALL 關鍵字；但如果使用者自訂函數是取決於 MDX 或 DMX 陳述式或指令碼內容中的物件 (例如目前的 Cube 或資料採礦模型)，則不可使用 CALL 關鍵字。 在 MDX 或 DMX 查詢之外呼叫函數的常見用途是使用 AMO 物件模型來執行管理功能。 例如，如果您想要在 MDX 陳述式中使用 `MyVoidProcedure(a, b, c)` 函數，就應使用下列語法：  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 組件的使用讓通用程式碼只需要開發一次，並儲存於單一位置，以簡化資料庫的開發。 用戶端軟體開發人員可針對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立函數程式庫，然後將它們和應用程式一起散發。  
  
 組件和使用者自訂函數可以重複 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 函數程式庫的函數名稱，或其他組件的函數名稱。 只要您使用完整名稱來呼叫使用者自訂函數， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會使用正確的程序。 基於安全性的理由，以及避免呼叫到不同類別庫中之重複名稱的可能性， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會要求您只使用預存程序的完整名稱。  
  
 若要從特定 CLR 組件呼叫使用者自訂函數，該使用者自訂函數將置於組件名稱、完整類別名稱，以及程序名稱之後，如下所示：  
  
 *AssemblyName*.*FullClassName*.*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 為了提供較早之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]版本的回溯相容性，亦可接受下列語法：  
  
 *AssemblyName*!*FullClassName*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 如果 COM 程式庫支援多重介面，則介面識別碼也可以用來解析程序名稱，如下所示：  
  
 *AssemblyName*!*InterfaceID*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
## <a name="security"></a>安全性  
 組件的安全性是以 .NET Framework 安全性模型為基礎，它是一種程式碼存取安全性模型。 .NET Framework 支援程式碼存取安全性機制，而這個機制假設執行階段可以主控完全信任和部份信任的程式碼。 受 .NET Framework 程式碼存取安全性保護的資源，一般都是以 Managed 程式碼包裝，而 Managed 程式碼在存取資源前會要求對應的權限。 唯有在呼叫堆疊中所有的呼叫者 (在組件層級) 都具有對應的資源權限時，權限的要求才會被滿足。  
  
 針對組件，執行的權限會透過 `PermissionSet` 物件的 `Assembly` 屬性傳遞。 Managed 程式碼所接收的權限是由實行中的安全性原則決定。 在非[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 主控環境中，已實行三個層級的原則：企業、電腦和使用者。 程式碼所接收的有效權限清單是由這三個層級所取得的權限交集決定。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在主控 CLR 時，會將主機層級的安全性原則層級提供給該 CLR；這項原則是位在永遠會實行之三個原則層級下的其他原則層級。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]建立的每一個應用程式網域都會設定此原則。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 主機層級原則，是系統組件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 固定原則，以及使用者組件的使用者指定原則的組合。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 主機原則之使用者自訂部份根據的是指定每個組件之下列其中一種權限值區 (共三種) 的組件擁有者：  
  
|權限設定|描述|  
|------------------------|-----------------|  
|`Safe`|提供內部計算權限。 這個權限值區不會指派權限，來存取 .NET Framework 中的所有受保護資源。 如果未使用 `PermissionSet` 屬性指定任何權限，這就會是組件的預設權限值區。|  
|`ExternalAccess`|提供和 `Safe` 設定相同的存取權，並附帶存取外部系統資源的能力。 這個權限值區不提供安全性保證 (雖然是可以確保此情況的安全)，但是可以提供可靠性的保證。|  
|`Unsafe`|不提供限制。 在此權限設定下執行的 Managed 程式碼，無法提供安全性或可靠性的保證。 任何權限，即使是管理員納入的自訂權限，皆可被授與在本信任層級執行的程式碼。|  
  
 當 CLR 是由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]主控時，以堆疊查核行程為基礎的權限檢查，就會在原生 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 程式碼的界限處停止。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組件中的任何 Managed 程式碼都一定會落入前面所列之三種權限類別目錄的其中一種。  
  
 COM (或 Unmanaged) 組件常式不支援 CLR 安全性模型。  
  
### <a name="impersonation"></a>模擬  
 只要 Managed 程式碼存取任何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 外部的資源時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會遵循與組件之 `ImpersonationMode` 屬性設定相關的規則，以確定該存取會發生在適當的 Windows 安全性內容中。 因為使用 `Safe` 權限設定的組件無法存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 外部的資源，所以這些規則僅適用於使用 `ExternalAccess` 和 `Unsafe` 權限設定的組件。  
  
-   如果目前的執行內容對應到 Windows 驗證的登入，且與原始呼叫者的內容相同 (即中間沒有 EXECUTE AS)，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在存取資源之前模擬 Windows 驗證的登入。  
  
-   如果有中繼 EXECUTE AS 變更了來自原始呼叫者的內容，對外部資源存取的嘗試就會失敗。  
  
 可將 `ImpersonationMode` 屬性設定為 `ImpersonateCurrentUser` 或 `ImpersonateAnonymous`。 預設值是 `ImpersonateCurrentUser`，會用來以目前使用者的網路登入帳戶執行組件。 如果`ImpersonateAnonymous`設定，則執行內容會對應至 Windows 登入使用者帳戶 IUSER_*servername*伺服器上。 這是網際網路 Guest 帳戶，在伺服器上的權限有限。 在這個內容中執行的組件，在本機伺服器上只能存取有限的資源。  
  
### <a name="application-domains"></a>應用程式網域  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不會直接公開應用程式定義域。 因為組件集是在相同的應用程式網域中執行，所以應用程式網域可以在執行時期使用 .NET Framework 中的 `System.Reflection` 命名空間或其他方式，來發現彼此，也可用延遲繫結方式呼叫它們。 這種呼叫會遭受以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 授權為基礎的安全性機制，進行權限檢查。  
  
 因為應用程式網域界限和每個網域中的組件都是由實作所定義，所以您不應該依賴在同一應用程式網域中尋找組件。  
  
## <a name="see-also"></a>另請參閱  
 [設定預存程序的安全性](../multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [定義預存程序](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
