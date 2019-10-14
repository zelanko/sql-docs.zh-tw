---
title: 建立入口網站品牌形象 | Microsoft Docs
ms.date: 04/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: 在本文中，您將了解如何透過品牌套件建立符合您企業的入口網站品牌形象，藉以變更入口網站的外觀。 品牌套件設計成不需要具備深度階層式樣式表 (CSS) 的知識，就能建立它。
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 47fc9ba65aca128a7e812f85c5bd06ca38131cbf
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251908"
---
# <a name="branding-the-web-portal"></a>建立入口網站品牌形象

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

您可以在入口網站上打造您的企業品牌形象，藉以變更入口網站的外觀。 這是透過品牌封裝來完成。 品牌套件設計成不需要具備深度階層式樣式表 (CSS) 的知識，就能建立它。

<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA" frameborder="0" allowfullscreen></iframe>

## <a name="creating-the-brand-package"></a>建立品牌封裝
  
Reporting Services 的品牌封裝包含三個項目且會封裝為 zip 檔案。   
  
- colors.json  
- metadata.xml  
- logo.png (選擇性)  
  
檔案必須具備上述的名稱。 不過您可以隨意命名 zip 檔案。  
  
### <a name="metadataxml"></a>metadata.xml
  
Metadata.xml 檔案可讓您設定品牌封裝的名稱，並擁有對 colors.json 和 logo.png 檔案的參考項目。  
  
若要變更品牌封裝的名稱，請變更 **SystemResourcePackage** 項目的 **name** 屬性。  
  
    name="Multicolored example brand"  
  
您可以選擇性地在品牌封裝中包含標誌圖片。 此項目會列於 Contents 項目中。  
  
不使用商標檔案的範例。  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
使用商標檔案的範例。  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### <a name="colorsjson"></a>Colors.json
  
上傳品牌封裝時，伺服器會從 colors.json 檔案擷取適當的名稱/值組，並將它們與主要的 LESS 樣式表合併 (brand.less)。 系統接著會處理這個 LESS 檔案，並將產生的 CSS 檔案提供給用戶端。 樣式表中的所有色彩都會遵循色彩的六個字元的十六進位表示法。  
  
LESS 樣式表所包含的區塊會參考某些預先定義的 LESS 變數，如下所示。  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
儘管這類似於 CSS 語法，但色彩值 (以 @symbol 作為首碼) 對 LESS 是唯一的。 它們是透過 json 檔案設定其值的變數。  
  
例如，如果 colors.json 檔案具有下列值。  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
已處理的輸出會查閱 **\@primaryButtonBg** 變數，且會看見它對應到名為 **primary** 的 json 屬性，在此範例中是 #009900。 因此，它就能輸出正確的 CSS。  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
所有的主要按鈕都會呈現深綠色以及白色文字。  
  
適用於 Reporting Services 的 Colors.json 檔案有兩個主要類別 (其中的項目已分組)。  
  
- **介面**︰包含 Reporting Services 入口網站特有的項目。  
- **佈景主題**︰包含您所建立的行動報表特有的項目。  
  
介面區段分成下列群組。  
  
|章節|描述|  
|---|---|  
|primary|按鈕和暫留色彩。|  
|次要|標題列、搜尋列、左邊功能表 (如果顯示) 及這些項目的文字色彩|  
|主要中性色彩|首頁和報表區域背景。|  
|次要中性色彩|文字方塊和資料夾選項背景，以及設定功能表。|  
|第三個中性色彩|站台設定背景。|  
|危險/警告/成功訊息|適用於這些訊息的色彩。|  
|KPI|將色彩控制為良好 (1)、中性 (0)、中性 (-1) 和無。|  
  
當第一次您連線到具備行動報表發行工具的伺服器時，該伺服器就已部署品牌封裝，而佈景主題將加入至您可在應用程式右上方功能表中使用的可用佈景主題。  
  
![ssRSBrandingMobileReportPublisher](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
接著可針對您建立的任何行動報表使用該佈景主題，即使它們不在您已部署該佈景主題的同一部伺服器上。   
  
### <a name="using-a-logo"></a>使用標誌
  
如果您在品牌封裝中包含標誌，則它會出現在入口網站中，來取代您在 [站台設定] 功能表中針對入口網站所設定的名稱。  
  
您針對標誌所納入的檔案必須使用 PNG 檔案格式。 檔案維度會在上傳至伺服器之後加以調整。 它應該會調整為大約 290px x 60px。  
   
## <a name="applying-the-brand-package-to-the-web-portal"></a>將品牌封裝套用至入口網站
  
若要加入、下載或移除品牌封裝，您可以執行下列動作。  
  
1.  選取右上方的**齒輪**。  
  
2.  選取 [網站設定]  。  
  
    ![ssRSGearMenu](../reporting-services/media/ssrsgearmenu.png)  
  
3.  選取 [建立品牌]  。  
  
    ![ssRSBranding](../reporting-services/media/ssrsbranding.png)  
  
**目前安裝的品牌封裝** 將顯示已上傳的封裝名稱，或顯示 [無]。  
  
**上傳品牌封裝** 會將封裝套用至入口網站。 您會看到它立即生效。  
  
您也可以 **下載** 或 **移除** 封裝。 移除封裝會立即將入口網站重設為預設品牌。  
  
## <a name="metadataxml-example"></a>metadata.xml 範例
  
    <?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="https://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
   
## <a name="colorsjson-example"></a>colors.json 範例
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  

## <a name="next-steps"></a>後續步驟

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
