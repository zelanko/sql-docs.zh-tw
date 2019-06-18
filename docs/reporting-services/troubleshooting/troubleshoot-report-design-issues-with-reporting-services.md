---
title: 針對 Reporting Services 的報表設計問題進行疑難排解 | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3eb298bc6b359b0df92566f9add8d7011cdc907
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573846"
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>疑難排解 Reporting Services 的報表設計問題
當您在報表撰寫應用程式中，以 [設計] 檢視建立報表配置時，可能會發生報表設計問題。 您可以使用本主題來協助疑難排解這些問題。   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>為什麼我的文字方塊只顯示一個值，而不在每一個資料列重複？  
一個具有資料集欄位參考的文字方塊，只會轉譯一次，並且顯示資料集中的前五個值。   
  
**文字方塊父項是報表主體**  
  
  
直接加到設計介面的文字方塊，只能顯示為資料集的彙總值。  
  
若要確認文字方塊的父容器，請選取該文字方塊，然後在 [屬性] 窗格中捲動至 **[Parent]** 。   
  
如果您需要文字方塊顯示資料集中的每一個值，請使用資料表或矩陣之類的資料區。 依預設，資料表或矩陣中的每個資料格都包含一個文字方塊。 將資料集欄位拖曳至各資料格。   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>為什麼無法在報表中加入總頁數？  
內建欄位 `[&PageNumber]` 和 `[&TotalPages]` 在報表主體中無效。   
  
PageNumber 和 TotalPages 只在頁首和頁尾有效。  
  
  
內建欄位 [&PageNumber] 和 [&TotalPages] 只在頁首和頁尾有效。   
  
若要將 [&PageNumber] 或 [&TotalPages] 加入至報表，您必須先新增頁首或頁尾。 如需相關資訊，請參閱[新增或移除頁面標頭](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
> 在頁首或頁尾中包含 [&TotalPages]，會對報表處理產生一些影響。 如需詳細資訊，請參閱「報表疑難排解：將報表匯出為特定檔案格式」。  
[疑難排解 Reporting Services 報表的處理](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md)。  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>如何設計兩個資料表，或是一個圖表和一個資料表，讓它們並排顯示？  
設計一份報表時，結果不一定是所見即所得。 報表處理器會結合資料、報表項目及報表配置資訊 (例如空白、容器和運算式) 以產生編譯報表，然後將報表傳送到報表轉譯器，根據您指定的檢視方式 (HTML 瀏覽器的互動式功能或是使用檔案格式) 來進行報表配置。 您可能需要變更由自動配置演算法所產生的報表配置。   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>轉譯規則會使用頁面大小、容器、對等物件、相對位置和空白來決定配置  
一般而言，報表會隨著資料增加而擴展其大小，並且將其他報表項目往旁邊推。   
  
若要將多個資料區或報表項目群組在一起，請將它們放在同一個父容器中。 例如，在矩形容器中放置圖表和資料表，然後對齊它們的上邊緣以並排顯示。 如需詳細資訊，請參閱 [報表產生器中的轉譯行為](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
[針對 Reporting Services 報表的資料擷取問題進行疑難排解](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[為 Reporting Services 訂閱與傳遞疑難排解](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

