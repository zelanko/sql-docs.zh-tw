---
title: 註冊資料庫元件對話方塊（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06647219ca5768495620bb1db60cf34910844f25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070464"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>註冊資料庫組件對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [註冊伺服器組件]**** 對話方塊，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中之組件參考的屬性。 在物件總管**** 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體或資料庫的 [組件] 資料夾，然後選取 [新增組件]****，即可顯示 [註冊伺服器組件]**** 對話方塊。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**類型**|顯示組件參考的類型。 有下列可用的值：<br /><br /> **.Net 元件**： <br />                      組件參考所參考的是 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 組件。<br /><br /> **COM DLL**： <br />                      組件參考所參考的是 COM 程式庫。<br /><br /> <br /><br /> ** \* \*安全性\*注意事項**COM 元件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。|  
|[檔案名稱]****|輸入 .NET 組件或 COM 程式庫的完整路徑和檔案名稱。|  
|**...**|按一下即可顯示 [開啟]**** 對話方塊，以選取 .NET 組件或 COM 程式庫的完整路徑和檔案名稱。|  
|**組件名稱**|輸入以設定組件參考的名稱。<br /><br /> 注意：變更此值並不會改變此組件參考所參考的組件名稱，但會變更 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體或資料庫在參考此組件參考時所使用的名稱。|  
|**包含偵錯資訊**|選取此選項即可包含 .NET 組件或 COM 程式庫的偵錯資訊 (如果有的話)。|  
|**建立時間戳記**|顯示建立組件參考的日期和時間。|  
|**上次結構描述更新**|顯示上次更新組件參考之中繼資料的日期和時間。|  
|**來源**|顯示組件參考的來源。 這個屬性通常包含組件參考所參考之組件的完整路徑和檔案名稱。|  
|**Safe**|選取此選項即可使用該組件參考的權限集合。 如果選取此選項，則組件只會允許內部計算及本機資料存取。 組件若以此選項執行程式碼，就無法存取外部系統資源，例如檔案、網路、環境變數或登錄。<br /><br /> ** \* \*安全性\*注意事項**對於執行計算和資料管理工作而不存取外部[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資源的元件而言，此選項是建議的許可權設定。 此選項代表最嚴格的權限集合。|  
|**外部存取**|選取此選項即可使用該組件參考的權限集合。 如果選取此選項，則組件只會允許內部計算及本機資料存取。 組件若以此權限集合執行程式碼，就可以存取外部系統資源，例如檔案、網路、環境變數及登錄。<br /><br /> ** \* \*安全性\*注意事項**對於存取外部[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資源的元件，建議使用此選項。 依預設，使用此選項的組件會以服務帳戶的安全認證來執行。 此元件中的程式碼可能會明確模擬呼叫者的[!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 驗證安全性內容。 由於預設會以服務帳戶的方式執行，因此使用此選項執行組件的權限，必須只提供給信任以服務帳戶執行的角色。 此選項代表的權限集合沒有 [安全]**** 嚴格，但比 [不受限制]**** 更嚴格。|  
|**L**|選取此選項即可使用該組件參考的權限集合。 如果選取此選項，組件就可以無限制地存取資源，包括內部和外部資源。 組件若使用此選項執行程式碼，就可以呼叫 Unmanaged 程式碼。<br /><br /> ** \* \*安全性\*注意事項**除非元件需要不受限制的存取權，否則不建議使用此選項。 就安全性的觀點而言，此選項與 [外部存取]**** 相同。 不過，使用 [外部存取]**** 選項的組件有提供各種可靠性和健全性的保護，這些是使用此選項的組件所缺乏的。 指定此選項即可允許組件中的程式碼在程序空間執行不合法作業，因此可能會危害 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的健全性和延展性。 此選項代表最不嚴格的權限集合，應該謹慎使用。|  
|**使用特定的使用者名稱和密碼**|選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用指定使用者帳戶的安全性認證。|  
|**使用者名稱**|輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的網域和名稱。 使用者帳戶的網域和名稱使用下列格式：<br /><br /> **\\** * \<功能變數名稱* *>\<使用者帳戶名稱>*<br /><br /> 注意：唯有選取 [Use a specific name and password (使用特定的使用者名稱和密碼)]**** 之後，才會啟用此選項。|  
|**密碼**|輸入選定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件所要使用之使用者帳戶的網域和名稱。|  
|**使用服務帳戶**|選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用與管理該物件之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服務相關聯的安全性認證。|  
|**使用目前使用者的認證**|選取此選項即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件使用目前使用者的安全性認證。|  
|**預設**|選取此選項即可使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的預設使用者帳戶。 選取此選項相當於選取 [使用目前使用者的認證]**** 選項。|  
|**描述**|輸入即可設定組件參考的描述。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型組件管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
