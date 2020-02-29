---
title: 建置、部署和偵錯自訂物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 89d1e2fd7c4f0e414424ad678c7ea9f3936b02f0
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176378"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>建立、部署和偵錯自訂物件
  撰寫 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之自訂物件的程式碼之後，必須建立並部署組件，以及將其整合到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具，其才可供封裝使用，並進行測試及偵錯。

##  <a name="top"></a> 針對 Integration Services 建置、部署和偵錯自訂物件的步驟
 您已經撰寫物件的自訂功能。 現在您必須測試它，並使其可供使用者使用。 其步驟非常類似於可以為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 建立之所有類型的自訂物件。

 以下是您在建立、部署及偵錯它時所要遵循的步驟：

1.  [簽署](#signing)要使用強式名稱產生的組件。

2.  [建置](#building)組件。

3.  將組件移至或複製至適當的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料夾，以[部署](#deploying)組件。

4.  在全域組件快取 (GAC) 中[安裝](#installing)組件。

     此物件會自動加入工具箱。

5.  必要時，可以為部署進行[疑難排解](#troubleshooting)。

6.  [測試](#testing)和偵錯您的程式碼。

##  <a name="signing"></a>簽署元件
 當要共用某個組件時，必須在全域組件快取中安裝它。 將組件加入至全域組件快取之後，類似 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的應用程式就可以使用該組件。 全域組件快取的要求是組件必須以強式名稱簽署，以確保組件是全域唯一的。 強式名稱的組件具有包含組件名稱、文化特性、公開金鑰和版本號碼的完整名稱。 執行階段會使用這項資訊找出該組件，並和其他同名的組件區別。

 若要使用強式名稱簽署組件，您必須先擁有或是建立公開/私密金鑰組。 這個公開和私密密碼編譯金鑰組將在建立時期用來建立強式名稱的組件。

 如需有關強式名稱以及簽署組件時必須遵循之步驟的詳細資訊，請參閱在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件中的下列主題：

-   強式名稱的組件

-   建立金鑰組

-   使用強式名稱簽署組件

 您可以在建立時期使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的強式名稱輕鬆地簽署組件。 在 [**專案屬性**] 對話方塊中，選取 [**簽署**] 索引標籤。選取 [**簽署元件**] 選項，然後提供金鑰（.snk）檔案的路徑。

##  <a name="building"></a>建立元件
 在簽署專案之後，您必須使用 ** 的 [建置]**[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 功能表上可用的命令，以建置或重建專案或是解決方案。 您的方案可能包含自訂使用者介面的個別專案，它也必須以強式名稱簽署，而且可以同時建立。

 執行接下來兩個步驟 (部署組件以及在全域組件快取中加以安裝) 的最方便方法，就是在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中將這些步驟撰寫成建置後事件。 建置事件可從 ** 專案上 [專案屬性] 的 [編譯]**[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 頁面取得，以及從 C# 專案的 [建置事件]**** 頁面取得。 
  **gacutil.exe** 這類的命令提示字元公用程式需要完整路徑。 凡包含空格的路徑，以及會使用到包含空格之路徑的巨集 (例如 $(TargetPath))，皆必須括以引號。

 以下是自訂記錄提供者的建置後事件命令列範例：

```
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\120\DTS\LogProviders "
```

##  <a name="deploying"></a>部署元件
 [!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具會藉由列舉在安裝時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]所建立的一系列資料夾中找到的檔案，來尋找可在封裝中使用的自訂物件。 使用預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝設定時，這組資料夾位於**C:\Program Files\Microsoft SQL Server\120\DTS**。 不過，如果您為自訂物件建立安裝程式，則應該檢查**HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\120\SSIS\Setup\DtsPath**登錄機碼的值，以確認此資料夾的位置。

 您可以透過下列兩種方式將組件放入資料夾中：

-   在建立編譯的組件之後，將它移動或複製到適當的資料夾  (為了方便起見，您可以在建置後事件中包括複製命令)。

-   直接在適當的資料夾中建置組件。

 **C:\Program FILES\MICROSOFT SQL Server\120\DTS**下的下列部署資料夾會用於各種類型的自訂物件：

|自訂物件|部署資料夾|
|-------------------|-----------------------|
|Task|工作|
|[ODBC 來源編輯器]|連接|
|記錄提供者|LogProviders|
|資料流程元件|PipelineComponents|

> [!NOTE]
>  將組件複製到這些資料夾中，以支援可用工作、連接管理員等項目的列舉。 因此，您不必將只包含自訂物件之自訂使用者介面的組件部署到這些資料夾。

##  <a name="installing"></a>將元件安裝在全域組件快取中
 若要將工作組件安裝至全域組件快取 (GAC)，請使用命令列工具 **gacutil.exe**，或是將組件拖曳至 `%system%\assembly` 目錄。 為了方便起見，您也可以在建置後事件中新增 **gacutil.exe** 呼叫。

 下列命令會使用 *gacutil.exe* 將名為 **MyTask.dll** 的元件安裝至 GAC。

 `gacutil /iF MyTask.dll`

 您必須在安裝新版本的自訂物件之後，關閉並重新開啟 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具。 如果您已在全域組件快取中安裝舊版的自訂物件，必須在安裝新版本之前先將之移除。 若要解除安裝組件，請執行 **gacutil.exe**，並使用 `/u` 選項指定組件名稱。

 如需全域組件快取的詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 工具中的全域組件快取工具 (Gactutil.exe)。

##  <a name="troubleshooting"></a>針對部署進行疑難排解
 如果您的自訂物件出現在 [工具箱]**** 或可用物件清單中，但您無法將它新增至套件，請嘗試下列動作：

1.  查詢全域組件快取，以取得元件的多個版本。 如果在全域組件快取中有多個版本的元件，設計師可能無法載入您的元件。 從全域組件快取中刪除此組件的所有執行個體，然後重新加入該組件。

2.  請確定部署資料夾中只包含一個該組件的執行個體。

3.  重新整理工具箱。

4.  將 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 附加至 **devenv.exe**，並設定中斷點，以逐步完成初始化程式碼，從而確保不會發生任何例外狀況。

##  <a name="testing"></a>測試和偵錯工具代碼
 在建置自訂物件以及執行可使用該元件的套件之後，從 ** 啟動 **dtexec.exe[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 是偵錯自訂物件之執行階段方法的最簡單方法。

 如果您想要對元件的設計階段方法（例如`Validate`方法）進行偵錯工具，請開啟使用第二個實例中之元件的封裝[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，並附加至其**devenv**進程。

 如果您也想要在套件於 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中開啟與執行時偵錯元件的執行階段方法，則必須在執行套件時強制暫停，才可附加到 **DtsDebugHost.exe** 處理序。

#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>附加到 dtexec.exe 偵錯物件的執行階段方法

1.  在偵錯組態中簽署和建立專案，然後加以部署，並將它安裝在全域組件快取中，如本主題所述。

2.  在 [**專案屬性**] 的 [**調試**程式] 索引標籤上，選取 [**啟動外部程式**] 作為 [**起始動作**]，並尋找預設安裝在 C:\Program Files\Microsoft SQL server\120\dts\binn 中的**dtexec .exe。**

3.  在 [命令列選項]**** 文字方塊的 [起始選項]**** 之下，輸入執行可使用您的元件之套件所需的命令列引數。 通常命令列引數是由 /F[ILE] 參數以及緊接在後面之 .dtsx 檔案的路徑與檔案名稱所組成。 如需詳細資訊，請參閱 [dtexec Utility](../packages/dtexec-utility.md)。

4.  在原始程式碼中設定中斷點，設定之處必須適合元件的執行階段方法。

5.  執行專案。

#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>若要將自訂物件的設計階段方法附加到 SQL Server Data Tools 以進行偵錯

1.  在偵錯組態中簽署和建立專案，然後加以部署，並將它安裝在全域組件快取中，如本主題所述。

2.  在原始程式碼中設定中斷點，設定之處必須適合自訂物件的設計階段方法。

3.  開啟第二個 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體，並載入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，該專案包含使用自訂物件的封裝。

4.  從第一個 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體的 [偵錯]**** 功能表中，選取 [附加至處理序]**** 載入套件，以從第一個執行個體附加到第二個 **devenv.exe** 執行個體。

5.  從第二個 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體執行封裝。

#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>若要將自訂物件的執行階段方法附加到 SQL Server Data Tools 以進行偵錯

1.  完成前一個程序所列的步驟之後，請強制暫停套件的執行，以附加到 **DtsDebugHost.exe**。 如果要強制執行此暫停動作，可以將中斷點加入 `OnPreExecute` 事件，或將指令碼工作加入專案，並輸入可顯示強制回應訊息方塊的指令碼。

2.  執行封裝。 暫停發生時，請切換至已開啟程式碼專案的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體，然後從 [偵錯]**** 功能表中選取 [附加至處理序]****。 請務必附加至 [類型]**** 資料行中列為 **Managed, x86** 的 **DtsDebugHost.exe** 執行個體，而不只是附加至列為 **x86** 的執行個體。

3.  返回暫停的套件並繼續略過中斷點，或是按一下 [確定]**** 以解除指令碼工作所引發的訊息方塊，然後繼續套件執行和偵錯。

![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [開發自訂物件以 Integration Services](developing-custom-objects-for-integration-services.md) [保存自訂物件](persisting-custom-objects.md)[疑難排解封裝開發的工具](../troubleshooting/troubleshooting-tools-for-package-development.md)


