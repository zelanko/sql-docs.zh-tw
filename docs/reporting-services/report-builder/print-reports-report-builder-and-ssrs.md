---
title: "列印報表 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e57d90ca72920722ddcf16d5d5708a782db5a71f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="print-reports-report-builder-and-ssrs"></a>列印報表 (報表產生器及 SSRS)
  將報表儲存至報表伺服器之後，您就可以從瀏覽器、報表管理員或任何用來檢視所匯出報表的應用程式，檢視及列印報表。 儲存報表之前，您可以在預覽報表時將它列印出來。  
  
 所有列印程序都可以視需要，直接在用戶端電腦上執行。 目前沒有伺服器端列印功能，可讓您從報表伺服器直接將列印工作傳送到連接 Web 伺服器的印表機。 印表機及列印選項是由個別的報表使用者，透過標準 **[列印]** 對話方塊加以選取。  
  
 特別為列印輸出設計報表的作者，可以使用分頁符號、頁首和頁尾、運算式和背景影像，來建立列印專用的報表設計。 供列印輸出使用的報表設計元素的範例，包括要列印在每一份報表背面的條款，或是模擬信頭的圖形和文字元素。  
  
 由於不同轉譯格式實作的分頁方式有所不同，您可能無法使每一份報表的每一種轉譯格式達到最佳列印輸出結果。 下列清單將提供範例：  
  
1.  報表頁面是為了容納不同資料量而設計的。 例如，依據使用者是否以互動方式切換資料列和資料行而定，包括矩陣的報表可能會造成頁面的橫向與縱向成長。 未擴充矩陣的使用者得到的列印結果，將與有擴充矩陣的使用者不同。  
  
2.  您無法在相同的報表中，合併橫向和縱向模式的頁面，也無法建立列印配置來取代在瀏覽器或其他應用程式中轉譯的報表配置或與之並存。  
  
3.  就大部分的匯出報表而言，報表列印輸出會包括報表上顯示的所有內容，如使用者在電腦螢幕上看到的一樣。 系統會保留報表設計介面中的空白。 若要以水平方式加入或移除額外的空白頁面，請變更報表頁面寬度。  
  
> [!NOTE]  
>  如果您使用瀏覽器的 [列印] 命令，則 HTML 報表列印輸出可能只會包含第一頁的內容。 如果您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用戶端列印功能來列印 HTML 報表，可以獲得較好的結果。 如需詳細資訊，請參閱 [使用列印控制項從瀏覽器列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>本節內容  
 [使用列印控制項從瀏覽器列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 描述如何使用用戶端列印功能，從網頁瀏覽器或報表管理員進行報表的列印。  
  
 [從其他應用程式列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
 描述如何列印已匯出至另一個應用程式的報表。  
  
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
 提供逐步指示，說明如何列印報表、如何控制頁面邊界，以及如何針對手動分頁轉譯器 (PDF、影像或列印) 所轉譯的報表指定紙張大小。  
  
## <a name="see-also"></a>請參閱＜  
 [匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
