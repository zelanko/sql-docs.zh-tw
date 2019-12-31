---
title: Analysis Services Multiidimensional 的全球化案例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7b0d6e4d99c08556cefb31c33deb5238f33c636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75225391"
---
# <a name="globalization-scenarios-for-analysis-services-multiidimensional"></a>Analysis Services 多維度的全球化案例
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]儲存及動作表格式和多維度資料模型中的多語系資料和中繼資料。 資料是以 Unicode (UTF-16) 儲存，也就是儲存在使用 Unicode 編碼的字元集中。 如果您將 ANSI 資料載入資料模型，則會使用對等的 Unicode 字碼指標來儲存字元。  
  
 Unicode 支援是指 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可使用 Windows 用戶端和伺服器作業系統支援的任何語言來儲存資料，並可讀取、寫入、排序及比較 Windows 電腦上所使用之任何字元集中的資料。 使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料的 BI 用戶端應用程式可以使用者選擇的語言來表示資料 (假設該語言的資料存在於模型中)。  
  
 語言支援對不同的人可能代表不同的意思。 下列清單可解決與 Analysis Services 如何支援語言相關的一些常見問題。  
  
-   如上所述，資料會儲存在 Windows 用戶端作業系統上任何以 Unicode 編碼的字元集中。  
  
-   中繼資料 (例如物件名稱、識別碼和描述) 也可以任何 Unicode 語言和字集來表示。 即使工具和環境使用另一種語言，也是如此。 例如，在整個堆疊使用英文和拉丁文定序的開發環境中，您可以在模型中包含其名稱使用斯拉夫文字元的物件。  
  
     標題和屬性成員可以翻譯表示 (僅限多維度模型)。 您可以定義一個或多個翻譯，然後再使用地區設定識別碼來決定要傳回用戶端的翻譯。 如需詳細資訊，請參閱下面的[功能](#bkmk_features)。  
  
-   從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎 (msmdsrv) 傳回的錯誤、警告和參考訊息已當地語系化為 Office 和 Office 365 支援的 43 種語言。 取得特定語言的訊息不需要進行設定。 用戶端應用程式的地區設定會決定要傳回的字串。  
  
-   組態檔 (msmdsrv.ini) 和 AMO PowerShell 只有英文版。  
  
-   記錄檔會包含英文和當地語系化訊息的混合 (假設您在 Analysis Services 執行所在的 Windows Server 上已安裝語言套件)。  
  
-   
  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 與 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]等文件與工具已翻譯成下列語言：簡體中文、繁體中文、法文、德文、義大利文、日文、韓文、葡萄牙文 (巴西)、俄文與西班牙文。 若要使用特定語言版本的工具，請安裝特定語言版本的 SQL Server (例如，安裝德文版 SQL Server 以取得德文版 Management Studio)，或執行目標語言之 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]的獨立安裝程式。  
  
 Analysis Services 可讓您在整個物件階層中獨立設定語言、定序和翻譯。  
  
 下列情況需要透過語言、定序和翻譯：  
  
-   一個提供多個翻譯標題的資料模型，讓欄位名稱和值可以使用者選擇的語言顯示。 針對加拿大、比利時或瑞士等雙語系國家/地區的營運公司，在不同的用戶端和伺服器應用程式之間支援多種語言是標準編碼需求。 在這種情況下，需要透過翻譯和貨幣轉換。 如需詳細資訊和連結，請參閱下面的 [功能](#bkmk_features) 。  
  
-   開發和生產環境位於不同的國家/地區。 在一個國家/地區開發方案，再部署至另一個國家/地區，變得愈來愈普遍。 如果您負責準備將使用某種語言開發的方案，部署至使用不同語言套件的伺服器，就必須了解如何設定語言和定序屬性。 設定這些屬性可讓您覆寫繼承並取自原始主機系統的預設值。 如需詳細資訊，請參閱下面的 [語言和定序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md) 。  
  
##  <a name="bkmk_features"></a>建立全球化多維度解決方案的功能  
 
  [!INCLUDE[applies](../includes/applies-md.md)] 僅限多維度資料模型  
  
 在用戶端層級，使用或操作 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度資料的全球化應用程式可使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的多語系和多重文化功能：  
  
-   [翻譯 &#40;Analysis Services&#41;](translations-analysis-services.md)是用來內嵌單一物件的多個標題，其中每個翻譯的字串都可以與其他翻譯並存。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ，為 Cube、量值、維度和屬性，定義標題、描述和帳戶類型的翻譯。 連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體時，您可以提供地區設定識別碼，從已定義翻譯的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件中擷取資料和中繼資料。  
  
     您可以在 [教學課程的](lesson-9-defining-perspectives-and-translations.md) 第 9 課：定義檢視方塊和翻譯 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，找到如何使用這項功能的課程。  
  
-   [貨幣轉換 &#40;Analysis Services&#41;](currency-conversions-analysis-services.md)是透過特製化的 MDX 腳本來轉換包含貨幣資料的量值。 您可以使用 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 中的 [商業智慧精靈] 來產生 MDX 指令碼，該指令碼使用維度、屬性和量值群組中的資料和中繼資料組合，來轉換含有貨幣資料的量值。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[語言和定序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)|指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的預設語言和 Windows 定序。 您的選擇會影響 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]所管理的資料和中繼資料。|  
|[翻譯 &#40;Analysis Services&#41;](translations-analysis-services.md)|定義 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫和資料庫所包含之物件的翻譯。 本主題說明 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 如何解析來自用戶端應用程式的翻譯資料和中繼資料要求。|  
|[貨幣轉換 &#40;Analysis Services&#41;](currency-conversions-analysis-services.md)|使用 [商業智慧精靈] 定義貨幣轉換。|  
|[&#40;Analysis Services 的全球化秘訣和最佳作法&#41;](globalization-tips-and-best-practices-analysis-services.md)|檢閱有助於避免發生與多語系資料相關之問題的幾個設計和編碼作法。|  
  
## <a name="see-also"></a>另請參閱  
 [Windows 應用程式的國際化](/windows/desktop/Intl/international-support)   
 [Microsoft 全球化檔](/globalization/)   
 [使用以地區設定為基礎的自動調整設計來撰寫 Windows Store 應用程式](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [使用 c # 和 XAML 開發通用 Windows 應用程式](https://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
