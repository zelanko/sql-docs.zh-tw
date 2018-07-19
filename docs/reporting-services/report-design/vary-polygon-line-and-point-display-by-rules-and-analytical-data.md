---
title: 使用規則與分析資料更改多邊形、線條與點顯示 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10538"
- "10537"
- sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10531"
- "10536"
- sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e78b0319639852d8bb4cac5be3f3b2157ac0703
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33027455"
---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data"></a>使用規則與分析資料更改多邊形、線條與點顯示
  地圖圖層上多邊形、線條與點的顯示選項是透過設定圖層的選項、設定圖層上地圖元素的規則，或是覆寫圖層上特定內嵌地圖元素的選項來控制。  
  
 顯示選項會以特定的優先順序套用 (從最低到最高)：  
  
1.  不論地圖元素是否內嵌在報表定義中，在多邊形圖層、線條圖層與點圖層上設定的選項都會套用到該圖層上的所有地圖元素。  
  
2.  針對規則設定的選項會套用到圖層上的所有地圖元素。 所有資料視覺效果選項都只會套用到與空間資料相關聯的地圖元素。 資料視覺效果選項會要求您指定資料欄位做為顯示變數的基礎。 您必須已經為分析資料與空間資料設定符合欄位，才能套用資料視覺效果規則。 如需詳細資訊，請參閱[地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)。  
  
3.  您為所選內嵌地圖元素設定的選項。 請注意，當您覆寫圖層選項時，您對報表定義所做的變更無法復原。 您可以變更資料欄位值，也可以覆寫顯示選項來自訂特定多邊形、線條和點顯示在圖層上的方式。  
  
 除了控制地圖元素在圖層上的顯示之外，您還可以控制圖層透明度，讓先前繪製的圖層透過稍後繪製的圖層顯示。 如需變更影響地圖或整個地圖圖層選項的詳細資訊，請參閱[自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> 了解規則  
 您可以設定四種類型的規則，讓報表處理器自動調整圖層上地圖元素的顯示屬性。 這些規則會隨著地圖元素類型而有所不同：多邊形、線條或點。  
  
-   **多邊形：** 更改多邊形色彩。  
  
    -   **多邊形中心點：** 針對在每個多邊形中心點顯示的標記，更改標記色彩、標記大小與標記類型。  
  
-   **線條：** 更改線條色彩與線條寬度。  
  
-   **點：** 對於每個點顯示的標記，更改標記色彩、標記大小與標記類型。  
  
##  <a name="Color"></a> 了解色彩規則  
 色彩規則會套用到多邊形、線條，以及代表點或多邊形中心點之標記的填滿色彩。  
  
 色彩規則支援以下四個選項：  
  
-   套用範本樣式： 您在精靈中選擇的主題會定義圖層的範本樣式。 設定字型樣式、框線樣式以及調色盤的主題。  
  
-   使用調色盤將資料視覺化： 您可以依名稱指定調色盤。 報表處理器會逐步執行調色盤中的每個色彩，然後在調色盤中連續套用每個色彩較淡的陰影，藉以設定圖層中每個地圖元素的色彩。  
  
-   使用色彩範圍將資料視覺化： 您可以指定開始色彩、中間色彩與結束色彩。 接著，您可以指定分佈選項。 報表處理器會使用分佈選項值來建立一組可顯示類似熱門地圖的色彩。 熱門地圖會將色彩顯示為與溫度相關。 例如，標尺為 0 到 100 時，最低值為藍色，代表冷；最高值為紅色，代表熱。  
  
-   使用自訂色彩將資料視覺化： 您可以指定一組色彩。 報表處理器會逐步執行您指定的值，藉以設定圖層中每個地圖元素的色彩。  
  
 預設調色盤包含白色。 為避免白色與調色盤中其他色彩之間的強烈對比，請指定一個開始色彩 (調色盤中的淡色)。  
  
 若要將與資料沒有關聯的地圖元素顯示為無色彩，請設定 **[無色彩]** 做為圖層上地圖元素的預設色彩。  
  
### <a name="color-scale"></a>色階  
 根據預設，所有色彩規則值除了出現在第一個圖例之外，也會出現在色階中。 色階是針對顯示一個範圍的色彩而設計。 在色階中選擇要顯示的最重要資料。  
  
 若要在色階中移除您不想要的值，請在每個圖層上清除每個色彩規則的色階選項。  
  
##  <a name="Width"></a> 了解線條寬度規則  
 寬度規則適用於線條。 寬度規則支援以下兩個選項：  
  
-   使用預設線條寬度。 您可以指定線條寬度 (以點為單位)。  
  
-   使用線條寬度將資料視覺化。 您可以設定線條的最小寬度與最大寬度、指定要使用的資料欄位來更改寬度，然後指定要套用到該資料的分佈選項。  
  
##  <a name="Size"></a> 了解標記大小規則  
 大小規則會套用到代表點或多邊形中心點的標記。 大小規則支援以下兩個選項：  
  
-   使用預設標記大小。 您可以指定大小 (以點為單位)。  
  
-   使用大小將資料視覺化。 您可以設定標記的最小大小與最大大小、指定要使用的資料欄位來更改大小，然後指定要套用到該資料的分佈選項。  
  
##  <a name="Marker"></a> 了解標記類型規則  
 標記類型規則會套用到代表點或多邊形中心點的標記。 標記類型規則支援以下兩個選項：  
  
-   使用預設標記類型。 您可以指定下列其中一種可用的標記類型。  
  
-   使用標記將資料視覺化。 您可以指定一組標記，然後指定您要使用這些標記的順序。 標記類型包括 **Circle**、 **Diamond**、 **Pentagon**、 **PushPin**、 **Rectangle**、 **Star**、 **Triangle**、 **Trapezoid**與 **Wedge**。  
  
##  <a name="Distribution"></a> 了解分佈選項  
 若要建立值的分佈，您可以將資料分割成幾個範圍。 您可以指定分佈類型、子範圍的數目，以及最小與最大範圍值。  
  
 在下列清單中，假設您有三個地圖元素和六個相關的分析值，其範圍為 1 到 9999，而其值分別為 1、10、200、2000、4777、8999。  
  
-   **EqualInterval：** 建立的範圍會將資料分割成相等的範圍間隔。 針對此範例，三個範圍為 0-2999、3000-5999、6000-8999。 子範圍 1：1、10、200、500。 子範圍 2：4777。 子範圍 3：8999。 此方法不會將資料分佈的方法納入考慮。 非常大的值或非常小的值都可能會扭曲分佈結果。  
  
-   **EqualDistribution：** 建立的範圍會分割該資料，讓每個範圍都有相等的項目數目。 針對此範例資料，三個範圍為 0-10、11-500、501-8999。 子範圍 1：1、10。 子範圍 2：200、500。 子範圍 3：4777、8999。 此方法可以建立跨越非常大範圍或非常小範圍的分佈來扭曲分佈。  
  
-   **最佳：** 建立會自動調整分佈的範圍來建立對稱的子範圍。 子範圍的數目取決於演算法。  
  
-   **自訂：** 指定您自己的範圍數目來控制值的分佈。 對於這些範例資料，您可以指定範圍 3 的範圍：1-2、3-8、9。  
  
 規則會使用分佈值來更改地圖元素顯示值。  
  
##  <a name="Legends"></a> 了解圖例與圖例項目  
 圖例項目是從針對每一個圖層指定的規則自動建立。 規則選項會控制建立的項目數目，以及其中會顯示的圖例。 根據預設，所有規則的所有項目都會加入至第一個圖例。 若要將項目移出第一個圖例，建立所需的額外圖例，然後針對每個規則指定要使用的圖例，來顯示規則所產生的項目。 若要根據規則隱藏項目，請指定一個空圖例名稱。  
  
 若要控制圖例顯示的位置，使用 [圖例屬性] 對話方塊來指定相對於地圖檢視區的位置。 如需詳細資訊，請參閱 [變更地圖圖例、色階與相關的規則 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)。  
  
 圖例會自動展開來顯示圖例標題或圖例文字。 若要格式化圖例項目的文字，使用地圖圖例關鍵字與自訂格式。 如需相關資訊，請參閱 [變更圖例中的內容格式](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems)。  
  
 下表顯示您可以使用之不同格式的範例。  
  
|關鍵字與格式|描述|在圖例中顯示為文字的範例|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|顯示沒有小數位數之總值的貨幣|$400|  
|`#FROMVALUE {C2}`|顯示兩個小數位數之總值的貨幣。|$400.55|  
|`#TOVALUE`|顯示資料欄位的實際數值。|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|顯示範圍開頭與範圍結尾的實際數值。|10 - 790|  
  
## <a name="see-also"></a>另請參閱  
 [變更地圖圖例、色階與相關的規則 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
