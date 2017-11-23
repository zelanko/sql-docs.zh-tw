---
title: "Analysis Services 的全球化案例 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c18f5e2ab55d1cae1f57ad67d157fc3f109949b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="globalization-scenarios-for-analysis-services"></a>Analysis Services 的全球化案例
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可儲存及操作表格式和多維度資料模型中的多語系資料和中繼資料。 資料是以 Unicode (UTF-16) 儲存，也就是儲存在使用 Unicode 編碼的字元集中。 如果您將 ANSI 資料載入資料模型，則會使用對等的 Unicode 字碼指標來儲存字元。  
  
 Unicode 支援是指 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可使用 Windows 用戶端和伺服器作業系統支援的任何語言來儲存資料，並可讀取、寫入、排序及比較 Windows 電腦上所使用之任何字元集中的資料。 使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料的 BI 用戶端應用程式可以使用者選擇的語言來表示資料 (假設該語言的資料存在於模型中)。  
  
 語言支援對不同的人可能代表不同的意思。 下列清單可解決與 Analysis Services 如何支援語言相關的一些常見問題。  
  
-   如上所述，資料會儲存在 Windows 用戶端作業系統上任何以 Unicode 編碼的字元集中。  
  
-   可以翻譯中繼資料，例如物件名稱。 雖然支援情形因模型類型而異，但多維度模型和表格式模型都支援模型內新增的已翻譯字串。 您可以定義多種翻譯，然後再使用地區設定識別碼來決定要傳回用戶端的翻譯。 如需詳細資訊，請參閱下面的 [功能](#bkmk_features)  
  
-   由 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎 (msmdsrv) 傳回的錯誤、警告和資訊訊息已當地語系化為 Office 和 Office 365 支援的 43 種語言。 取得特定語言的訊息不需要進行設定。 用戶端應用程式的地區設定會決定要傳回的字串。  
  
-   組態檔 (msmdsrv.ini) 和 AMO PowerShell 只有英文版。  
  
-   記錄檔會包含英文和當地語系化訊息的混合 (假設您在 Analysis Services 執行所在的 Windows Server 上已安裝語言套件)。  
  
-   [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 與 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]等文件與工具已翻譯成下列語言：簡體中文、繁體中文、法文、德文、義大利文、日文、韓文、葡萄牙文 (巴西)、俄文與西班牙文。 在安裝期間可指定文化特性 (Culture)。  
  
 若為多維度模型，Analysis Services 可讓您在整個物件階層中獨立設定語言、定序和翻譯。  若為表格式模型，您可以只加入翻譯︰語言和定序則繼承自主機作業系統。  
  
 透過 Analysis Services 全球化功能的可能案例包括︰  
  
-   一個提供多個翻譯標題的資料模型，讓欄位名稱和值可以使用者選擇的語言顯示。 針對加拿大、比利時或瑞士等雙語系國家/地區的營運公司，在不同的用戶端和伺服器應用程式之間支援多種語言是標準編碼需求。 在這種情況下，需要透過翻譯和貨幣轉換。 如需詳細資訊和連結，請參閱下面的 [功能](#bkmk_features) 。  
  
-   開發和生產環境位於不同的國家/地區。 在一個國家/地區開發方案，再部署至另一個國家/地區，變得愈來愈普遍。 如果您負責準備將使用某種語言開發的方案，部署至使用不同語言套件的伺服器，就必須了解如何設定語言和定序屬性。 設定這些屬性可讓您覆寫繼承並取自原始主機系統的預設值。 如需詳細資訊，請參閱下面的 [語言和定序 &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md) 。  
  
##  <a name="bkmk_features"></a> 建立全球化多語系方案的功能  
 在用戶端層級，使用或操作 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度資料的全球化應用程式可使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的多語系和多重文化功能。  
  
 連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體時，您可以提供地區設定識別碼，從已定義翻譯的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件中擷取資料和中繼資料。  
  
 如需有助於避免發生多語系資料相關問題的設計和編碼做法，請參閱[全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)。  
  
||||  
|-|-|-|  
|**功能**|**表格式**|**多維度**|  
|[語言和定序 &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)|繼承自作業系統。|是繼承的，但能覆寫模型階層中主要物件的語言和定序。|  
|翻譯支援的範圍|標題和描述。|可以為物件名稱、標題、識別碼和描述建立翻譯，也可以任何 Unicode 語言和指令碼表示。 即使工具和環境使用另一種語言，也是如此。 例如，在整個堆疊使用英文和拉丁文定序的開發環境中，您可以在模型中包含其名稱使用斯拉夫文字元的物件。|  
|實作翻譯支援|使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立，以產生您填入並匯回模型中的翻譯檔案。<br /><br /> 如需詳細資訊，請參閱[表格式模型中的翻譯 &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)。|使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立，以定義標題和描述的翻譯，以及 Cube、量值、維度及屬性的帳戶類型。<br /><br /> 如需詳細資訊，請參閱[多維度模型中的翻譯 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)。 您可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程的[第 9 課：定義檢視方塊和翻譯](../analysis-services/lesson-9-defining-perspectives-and-translations.md)中，找到如何使用這項功能的課程。|  
|貨幣轉換|無法使用。|貨幣轉換是透過特製化的 MDX 指令碼，來轉換含有貨幣資料的量值。 您可以使用 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 中的 [商業智慧精靈] 來產生 MDX 指令碼，該指令碼使用維度、屬性和量值群組中的資料和中繼資料組合，來轉換含有貨幣資料的量值。 請參閱[貨幣轉換 &#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md)。|  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 中的翻譯支援](../analysis-services/translation-support-in-analysis-services.md)   
 [Windows 應用程式的國際化](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Go Global 開發人員中心](http://msdn.microsoft.com/goglobal/bb871628.aspx)   
 [使用地區設定為基礎的自動調整設計撰寫 Windows 市集應用程式](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [開發通用 Windows 應用程式與 C# 和 XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
