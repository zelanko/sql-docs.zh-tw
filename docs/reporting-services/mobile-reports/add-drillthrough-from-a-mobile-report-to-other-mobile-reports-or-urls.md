---
title: "從行動報表的鑽研加入到其他行動報表或 Url |Microsoft 文件"
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30d0a3fd-5588-417e-b25d-cc5b7624cdb1
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c00b90770f259d9782c68eec52ccf860762f43f1
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls"></a>從行動報表將鑽研加入其他行動報表或 URL
您可以從 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表中的任何量測計、圖表或資料格將鑽研加入另一個行動報表或自訂 URL。 

「鑽研」是來源報表中開啟另一個目標報表或 URL 的連結。 目標鑽研報表通常包含摘要報表中某個項目的詳細資料。 根據來源行動報表，可以將一或多個參數傳遞至目標行動報表或整合至自訂 URL。  
  
如果在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web 入口網站中檢視來源行動報表，並且選取具有鑽研目標的元素，您可以移至該目標 (另一個行動報表或 URL)。  

具有 URL 或其他行動報表鑽研的報表項目，在右上角 ![mobile-report-drill-through-icon](../../reporting-services/mobile-reports/media/mobile-report-drill-through-icon.png) 會有鑽研圖示。

![mobile-report-gauge-drill-through](../../reporting-services/mobile-reports/media/mobile-report-gauge-drill-through.png) 

>**提示**：建立目標報表，並先將它儲存到 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web 入口網站。 如果您打算傳遞來源報表中的參數，亦請一併將參數加入目標報表中。 您接著可以設定從來源報告鑽研到目標報表。 [將參數加入行動報表中](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).
 
## <a name="set-up-drillthrough-to-a-mobile-report"></a>設定鑽研到行動報表  

1. 在 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]的配置檢視中，選取可支援鑽研的視覺效果。   

   地圖和量測計支援鑽研，就像大部分的圖表和簡單資料格一樣。
   
2. 在 [視覺屬性] 窗格中，選取 [鑽研目標] > [行動報表]。  
3. 選取伺服器和目標行動報表。  

   >注意︰如果目標行動報表不是與來源行動報表位在相同的伺服器上，請改用自訂 URL 來連接它 (如下節所述)。  
 
4. 在您選取目標行動報表之後，會看到其可用的輸入參數，包括可繫結至目標行動報表資料集上所設定的導覽器控制項和參數的屬性。  

   ![mobile-report-drillthrough-target](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-target.PNG)
   
   *目標行動報表的鑽研屬性*  
  
5. 選取每個屬性右側的箭頭，將具有相符資料類型的屬性連接至來源行動報表上的可用輸出屬性。 如果報表使用者在鑽研到目的地行動報表之前尚未與來源行動報表互動，則您也可以在這裡設定每個輸出的預設值。  
  
## <a name="set-up-a-drillthrough-to-a-custom-url"></a>設定鑽研到自訂 URL  
  
1. 在 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 的配置檢視中，選取可支援鑽研目標的視覺效果。    
2. 在 [視覺屬性] 窗格中，選取 [鑽研目標] > [自訂 URL]。  這樣會開啟鑽研組態對話方塊。  
  
3. 在 [設定鑽研 URL] 中，輸入要在按一下視覺效果時前往的目的地 URL，然後從右側所列的 [可用參數] 中進行選取。 下列面板會顯示與範例解析參數 (如果包括的話) 合併之自訂 URL 的預覽。  
  
   ![mobile-report-drillthrough-url](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-url.PNG)
  
   *鑽研到自訂 URL 屬性*  
  
4. 按一下 **[套用]**。  

  
當您在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]中預覽行動報表時，如果按一下具有鑽研的視覺效果，則會看到停用鑽研的訊息。 在您儲存或發行行動報表並進行檢視之後，實際上只能鑽研到目標，而不是在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 配置或預覽模式中。  

## <a name="hide-a-target-mobile-report-on-the-web-portal"></a>在 Web 入口網站上隱藏目標行動報表
如果您不打算要設定目標報表的預設值，請考慮在 Web 入口網站上予以隱藏。 否則，如果有人嘗試直接在 Web 入口網站上檢視它，而不是透過來源報表，則它會是空白。

1. 在 Web 入口網站中，於您要隱藏的目標報表上選取省略符號 (...)，然後選取 [管理]。

2. 在 [內容] 中，選取 [在並排顯示檢視中隱藏]。

您可以選擇檢視 Web 入口網站中的隱藏項目︰ 

* 在 Web 入口網站的右上方，選取 [檢視] > [顯示隱藏項]。 

隱藏的項目會以較淡的色彩顯示。
    
### <a name="see-also"></a>另請參閱  
 
* [將參數加入 Reporting Services 行動報表中](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [使用 SQL Server 行動報表發行工具建立行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 
* [Web 入口網站 （SSRS 原生模式）](../../reporting-services/web-portal-ssrs-native-mode.md)


