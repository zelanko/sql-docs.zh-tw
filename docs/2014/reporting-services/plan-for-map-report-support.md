---
title: 對應報表支援規劃 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 44b196d9c8ff508e6a878d51000bea95d8011907
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293917"
---
# <a name="plan-for-map-report-support"></a>對應報表支援規劃
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 支援使用空間資料來源的地圖報表。 空間資料可以來自 SQL Server 資料庫、ESRI 形狀檔，或是隨著 Reporting Services 或報表產生器一起安裝的地圖庫。 地圖也可以顯示 Bing 地圖底圖的背景。 報表作者可以建立報表，做為動態，在執行階段擷取或為 static 並內嵌在報表定義中指定空間資料或 Bing 地圖底圖。  
  
## <a name="support-for-bing-maps"></a>Bing Map 的支援  
 地圖可以包含顯示 Bing 地圖底圖的背景圖層。 若要檢視具有地圖底圖圖層的已發行報表，報表伺服器必須設定為可從 Bing Maps Web 服務擷取圖格。 如需詳細資訊，請參閱 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)。  
  
 在每個報表中，報表作者也可以指定是否要使用安全通訊端層 (SSL) 連線，自圖格伺服器擷取圖格。 若要這樣做，在圖格圖層的 [屬性] 窗格中，它們必須將 usesecureconnection 設定布林屬性設定到`true`。  
  
> [!NOTE]  
>  如需有關在報表中使用 Bing 地圖底圖的詳細資訊，請參閱 [其他使用規定](https://go.microsoft.com/fwlink/?LinkId=151371) 和 [隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=151372)。  
  
## <a name="report-design-recommendations"></a>報表設計建議  
 好的地圖報表設計需要報表作者評估靜態與動態空間資料之間的權衡得失，並找出平衡點來服務報表使用者。 內嵌的地圖元素可能會大幅增加報表定義的大小，但是會減少檢視地圖報表所需的時間。 動態地圖元素會減少報表定義的大小，但是會增加處理及檢視地圖所需的時間。 報表作者必須找到這些對立問題之間的平衡點。  
  
 當報表定義大小是一個問題時，身為報表伺服器管理員的您可以鼓勵報表設計師減少報表定義中的空間資料數量。  
  
 在下列情況下，地圖元素會內嵌在報表定義中：  
  
-   建立報表時，空間資料來源位於本機檔案系統上。 其中包括來自地圖庫的空間資料，或是已經安裝在本機的 ESRI 形狀檔。 根據預設，地圖精靈和地圖圖層精靈會內嵌本機檔案系統上資料來源中的空間資料。  
  
-   報表作者可選擇以手動方式將空間資料內嵌在報表中。  
  
 若要減少具有地圖的報表定義大小，報表作者可以使用下列其中一個或多個選項：  
  
-   從 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的報表設計師，將屬於 ESRI 形狀檔的空間資料來源加入至報表伺服器專案。 當您部署此專案時，ESRI 形狀檔除了發行至報表中，也會發行至報表伺服器。 當報表作者執行地圖精靈時，他們可以從報表伺服器專案指定空間資料來源，而地圖元素預設不會內嵌到報表定義中。  
  
-   在報表產生器中，從報表伺服器選取形狀檔，加入屬於 ESRI 形狀檔的空間資料來源。 當報表作者執行地圖精靈時，可以從報表伺服器瀏覽並選取空間資料來源，而地圖元素是預設為不會內嵌到報表定義中。  
  
-   當地圖資料必須為內嵌的地圖資料時，請調整檢視區置中與縮放比例，以便只包含報表所需的地圖資料。  
  
 如需詳細資訊， [Maps&#40;報表產生器及 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表疑難排解：將報表對應&#40;報表產生器及 SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
