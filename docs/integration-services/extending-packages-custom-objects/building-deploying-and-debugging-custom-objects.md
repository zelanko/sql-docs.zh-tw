---
title: "建置、 部署和偵錯自訂物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>建立、部署和偵錯自訂物件
  您撰寫的自訂物件的程式碼完成之後[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，您必須建置組件、 部署，並將其整合到[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具，使其可供使用中的套件和測試及偵錯。  
  
##  <a name="top"></a>建置、 部署和整合服務的偵錯自訂物件中的步驟  
 您已經撰寫物件的自訂功能。 現在您必須測試它，並使其可供使用者使用。 其步驟非常類似於可以為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 建立之所有類型的自訂物件。  
  
 以下是建置、 部署和測試的步驟。  
  
1.  [符號](#signing)要產生強式名稱組件。  
  
2.  [建置](#building)組件。  
  
3.  [部署](#deploying)移動或複製到適當的組件[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]資料夾。  
  
4.  [安裝](#installing)全域組件快取 (GAC) 中的組件。  
  
     此物件會自動加入工具箱。  
  
5.  [疑難排解](#troubleshooting)如有必要的部署。  
  
6.  [測試](#testing)和偵錯您的程式碼。  
  
 您現在可以使用 SSIS 設計師中 SQL Server Data Tools (SSDT) 來建立、 維護及執行不同的版本為目標的封裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需這項改進您的自訂擴充功能上的影響的詳細資訊，請參閱[取得 SSIS 自訂擴充功能必須支援多個版本支援的 SSDT 2015 的 SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>簽署組件  
 當要共用某個組件時，必須在全域組件快取中安裝它。 將組件加入至全域組件快取之後，類似 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的應用程式就可以使用該組件。 全域組件快取的要求是組件必須以強式名稱簽署，以確保組件是全域唯一的。 強式名稱的組件具有包含組件名稱、文化特性、公開金鑰和版本號碼的完整名稱。 執行階段會使用這項資訊找出該組件，並和其他同名的組件區別。  
  
 若要使用強式名稱簽署組件，您必須先擁有或是建立公開/私密金鑰組。 這個公開和私密密碼編譯金鑰組將在建立時期用來建立強式名稱的組件。  
  
 如需有關強式名稱以及簽署組件時必須遵循之步驟的詳細資訊，請參閱在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件中的下列主題：  
  
-   強式名稱的組件  
  
-   建立金鑰組  
  
-   使用強式名稱簽署組件  
  
 您可以在建立時期使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的強式名稱輕鬆地簽署組件。 在**專案屬性**對話方塊中，選取**簽署** 索引標籤。 選取的選項**簽署組件**，然後提供金鑰 (.snk) 檔案的路徑。  
  
##  <a name="building"></a>建置組件  
 專案之後，您必須建置，或使用上可用的命令來重建專案或方案**建置**功能表[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。 您的方案可能包含自訂使用者介面的個別專案，它也必須以強式名稱簽署，而且可以同時建立。  
  
 執行後續兩個步驟 (部署組件以及在全域組件快取中安裝它) 的最方便的方法，就是在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中將這些步驟撰寫成建置後事件。 建置事件都是從**編譯**專案屬性的頁面[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]專案，並從**建置事件**C# 專案的頁面。 完整路徑是必要的命令提示字元公用程式，例如**gacutil.exe**。 凡包含空格的路徑，以及會使用到包含空格之路徑的巨集 (例如 $(TargetPath))，皆必須括以引號。  
  
 以下是自訂記錄提供者的建置後事件命令列範例：  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>部署組件  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具依找出可供使用的自訂物件中封裝列舉一系列時，會建立的資料夾中找到的檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安裝。 當預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝設定，這組資料夾位於之下**C:\Program Files\Microsoft SQL Server\130\DTS**。 不過如果您建立安裝程式的自訂物件時，您應該檢查的值**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath**登錄機碼，以確認此資料夾的位置。  
  
> [!NOTE]  
>  如需如何部署與 SQL Server Data Tools 中的多個版本支援的自訂元件的資訊，請參閱[取得 SSIS 自訂擴充功能必須支援 SQL Server 2016 的多個版本支援的 SSDT 2015](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)。  
  
 您可以透過下列兩種方式將組件放入資料夾中：  
  
-   在建立編譯的組件之後，將它移動或複製到適當的資料夾  (為了方便起見，您可以在建置後事件中包括複製命令)。  
  
-   直接在適當的資料夾中建置組件。  
  
 下列部署資料夾下的**C:\Program Files\Microsoft SQL Server\130\DTS**用於各種類型的自訂物件：  
  
|自訂物件|部署資料夾|  
|-------------------|-----------------------|  
|工作|工作|  
|[ODBC 目的地編輯器]|連接|  
|記錄提供者|LogProviders|  
|資料流程元件|PipelineComponents|  
  
> [!NOTE]  
>  將組件複製到這些資料夾中，以支援可用工作、連接管理員等項目的列舉。 因此，您不必將只包含自訂物件之自訂使用者介面的組件部署到這些資料夾。  
  
##  <a name="installing"></a>在全域組件快取中安裝組件  
 若要將工作組件安裝到全域組件快取 (GAC) 中，使用命令列工具**gacutil.exe**，或拖曳至組件`%system%\assembly`目錄。 為了方便起見，您也可以包含在呼叫**gacutil.exe**建置後事件中。  
  
 下列命令安裝元件，名為*MyTask.dll*使用 gac **gacutil.exe**。  
  
 `gacutil /iF MyTask.dll`  
  
 您必須在安裝新版本的自訂物件之後，關閉並重新開啟 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具。 如果您已在全域組件快取中安裝舊版的自訂物件，必須在安裝新版本之前先將之移除。 若要解除安裝組件，請執行**gacutil.exe**和指定的組件名稱與`/u`選項。  
  
 如需全域組件快取的詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 工具中的全域組件快取工具 (Gactutil.exe)。  
  
##  <a name="troubleshooting"></a>疑難排解部署  
 如果您的自訂物件出現在**工具箱**或清單中的可用物件中，但您不能將它加入至封裝，請嘗試下列：  
  
1.  查詢全域組件快取，以取得元件的多個版本。 如果在全域組件快取中有多個版本的元件，設計師可能無法載入您的元件。 從全域組件快取中刪除此組件的所有執行個體，然後重新加入該組件。  
  
2.  請確定部署資料夾中只包含一個該組件的執行個體。  
  
3.  重新整理工具箱。  
  
4.  附加[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]至**devenv.exe** ，並設定中斷點來逐步執行程式的初始化程式碼，以確保發生任何例外狀況。  
  
##  <a name="testing"></a>測試和偵錯您的程式碼  
 偵錯自訂物件的執行階段方法最簡單的方式是開始**dtexec.exe**從[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]之後建置您的自訂物件，並執行使用之元件的封裝。  
  
 如果您想要偵錯元件的設計階段方法，例如**驗證**方法中，開啟使用中的第二個執行個體元件的封裝[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，並附加至其**devenv.exe**程序。  
  
 如果您也想要偵錯元件的執行階段方法，當開啟與執行封裝[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具，您必須強制暫停封裝的執行，因此您也可以附加至**DtsDebugHost.exe**程序。  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>附加到 dtexec.exe 偵錯物件的執行階段方法  
  
1.  在偵錯組態中簽署和建立專案，然後加以部署，並將它安裝在全域組件快取中，如本主題所述。  
  
2.  在**偵錯** 索引標籤**專案屬性**，選取**啟動外部程式**為**起始動作**，並找出**dtexec.exe**，這預設安裝在 C:\Program Files\Microsoft SQL Server\130\DTS\Binn。  
  
3.  在**命令列選項**文字方塊中，在**起始選項**，輸入執行的封裝，使用您的元件所需的命令列引數。 通常命令列引數是由 /F[ILE] 參數以及緊接在後面之 .dtsx 檔案的路徑與檔案名稱所組成。 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。  
  
4.  在原始程式碼中設定中斷點，設定之處必須適合元件的執行階段方法。  
  
5.  執行您的專案。  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>若要將自訂物件的設計階段方法附加到 SQL Server Data Tools 以進行偵錯  
  
1.  在偵錯組態中簽署和建立專案，然後加以部署，並將它安裝在全域組件快取中，如本主題所述。  
  
2.  在原始程式碼中設定中斷點，設定之處必須適合自訂物件的設計階段方法。  
  
3.  開啟第二個 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體，並載入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，該專案包含使用自訂物件的封裝。  
  
4.  從第一個執行個體[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，附加至第二個執行個體**devenv.exe**在封裝載入選取**附加至處理序**從**偵錯**功能表第一個執行個體。  
  
5.  從第二個 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體執行封裝。  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>若要將自訂物件的執行階段方法附加到 SQL Server Data Tools 以進行偵錯  
  
1.  您已完成之前程序中所列的步驟之後，強制暫停封裝的執行，讓您可以附加至**DtsDebugHost.exe**。 您可以藉由新增中斷點，以強制執行此暫停**OnPreExecute**事件，或將指令碼工作加入至您的專案，然後輸入顯示強制回應的訊息方塊的指令碼。  
  
2.  執行封裝。 當暫停發生時，切換至執行個體[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]中的程式碼專案會開啟，並選取**附加至處理序**從**偵錯**功能表。 請務必附加至執行個體**DtsDebugHost.exe**列為**Managed，x86**中**類型**資料行，不屬於執行個體列為**x86**只。  
  
3.  返回暫停的封裝並繼續略過中斷點，或者按一下**確定**解除指令碼工作中，所引發的訊息方塊，並繼續封裝執行和偵錯。  
  
## <a name="see-also"></a>另請參閱  
 [開發 Integration Services 自訂物件](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [保存自訂物件](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [疑難排解封裝開發的工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
