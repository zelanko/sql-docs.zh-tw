---
title: Reporting Services 行動報表中的地圖 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1fbb2ad5c2c652f5be04982ffaedb7eadea97be
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294776"
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Reporting Services 行動報表中的地圖
地圖是將地理資料視覺化的最佳方式。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 提供三種不同類型的地圖視覺效果，以及針對各大洲和一些個別國家/地區內建的地圖。 您也可以 [上傳和使用自訂的地圖](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)。   
  
## <a name="types-of-maps"></a>地圖類型  
  
SQL Server 行動報表提供三種不同類型的地圖，適用於各種不同的情況。  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**漸層熱度圖** [值] 屬性中的欄位會顯示為填滿地圖中每個區域的單色網底。 您可以在 [值方向] 方塊中，設定較高或較低的值是否比較暗。  
  
**泡泡地圖** [值] 屬性會決定在相關區域上顯示的泡泡視覺效果的半徑。 您可以設定所有泡泡的色彩是否都一樣或完全不同。   
  
**範圍填滿熱度圖** 會顯示與目標相關的值。 [目標] 屬性會決定 [比較] 欄位和 [值] 欄位之間的差異。 產生的差異會決定要填滿地圖相關區域的色彩 (從綠色、黃色到紅色)。 您可以在 [值方向] 方塊中，設定較高或較低的值是否為綠色。  
  
## <a name="select-the-map-type-and-region"></a>選取地圖類型和區域  
  
1. 在 [配置] 索引標籤上選取地圖類型、將它拖曳至設計介面，並調整為您想要的大小。  
  
2. 在 [配置] 檢視 > [視覺屬性] 面板 > [地圖] 中，選取您所需的特定地圖區域。  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. 針對漸層和範圍填滿熱度圖，在 [視覺屬性] 下方的 [值方向] 中設定較高或較低的值是否比較好。  
  
7. 針對泡泡地圖，在 [視覺屬性] 下方，將 [使用不同色彩] 設定為 [開啟] 或 [關閉]，使所有泡泡的色彩都一樣或完全不同。  
  
## <a name="select-the-map-data"></a>選取地圖資料  
當您第一次將地圖加入報表時， [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 會填入模擬的地理資料。  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
若要在地圖中顯示實際資料，您至少需要為兩個地圖的資料屬性設定值︰   
* [索引鍵] 屬性會將資料連接到特定的地圖區域 -- 例如，美國各州或非洲國家/地區。  
* [值] 屬性是與所選取索引鍵欄位處於相同資料表的數值欄位。 這些值在不同的地圖中有不同的表示方式。 **漸層圖** 會使用這些值，根據值範圍，使用各種不同的網格來為每個區域上色。 **泡泡地圖** 會根據值屬性，來設定每個區域中泡泡視覺效果的大小。   
* 針對範圍填滿熱度圖，您也需要設定 [目標] 屬性。  
  
### <a name="set-map-data-properties"></a>設定地圖資料屬性  
  
1. 選取左上角的 [資料] 索引標籤。  
  
2. 選取 [Add Dat] (新增資料)，然後選取 [本機 Excel] 或 [SSRS 伺服器]。  
  
   > **提示**：請確定[資料格式適用於行動報表](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)。  
  
3. 選取所需的工作表，然後選取 [匯入]。  
   您會在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]中看見您的資料。  
  
4. 在這個 [資料] 檢視 > [資料屬性] 面板 > [索引鍵] 下方的左側方塊中，選取包含地圖資料的資料表，並在右側方塊中選取符合您地圖區域的索引鍵欄位。  
  
5. 在 [值] 下方，相同的資料表已存在於左側方塊中。 選取您想要在地圖上顯示其值的數值欄位。   
  
6. 如果這是範圍填滿熱度圖，則在 [目標] 方塊下方，會有相同的資料表存在於左側方塊中。 在右側方塊中，選取您想要將其值做為目標的數值欄位。   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. 選取左上角的 [預覽]。  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. 選取左上角的 [儲存] 圖示，以及 [本機儲存] 於您的電腦上或 [儲存到伺服器]。  
  
### <a name="see-also"></a>另請參閱  
-  [Reporting Services 行動報表中的自訂地圖](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  
