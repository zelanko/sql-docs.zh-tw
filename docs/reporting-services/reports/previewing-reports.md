---
title: "預覽報表，|Microsoft 文件"
ms.custom: 
ms.date: 05/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45df97d21abc1ac494592c98e69964a38d7f4d21
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="previewing-reports"></a>預覽報表
  設計     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表時，在尚未發行至實際環境之前，您可能會想要先檢視該報表。 您可以利用數種方式進行檢視：在報表設計師中切換到 [預覽] 模式、使用報表設計師中的預覽視窗，以及在測試環境中將報表發行至報表伺服器。  
  
> [!NOTE]  
>  預覽報表時，報表的資料會快取至本機電腦上的檔案。 當您再次預覽同一份報表時 (使用相同的查詢、參數和認證)，報表設計師會擷取快取複本，而非重新執行查詢。 資料檔案儲存為 *\<reportname >*。.rdl.data 與報表定義檔案相同的目錄中。 您關閉報表設計師時，不會刪除此檔案。  
  
## <a name="preview-mode"></a>預覽模式  
 您可以預覽報表在報表設計師中的，依序按一下![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview")。 這會在本機執行報表，使用與報表伺服器相同的報表處理與轉譯功能。 顯示的報表是互動式影像；您可以選取參數、按一下連結、檢視文件引導模式，以及展開和摺疊報表的隱藏區域。 您也可以將報表匯出至任何已安裝的轉譯格式。  
  
## <a name="standalone-preview"></a>獨立預覽  
 另一個預覽報表的方式是在偵錯組態下執行報表專案，例如，偵錯您撰寫的自訂組件。 報表會在預設瀏覽器中開啟。 有三種方法可以執行專案：  
  
-   在 [偵錯] 功能表中，按一下 [開始偵錯]。  
  
-   依序按一下**啟動**按鈕[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)][標準] 工具列![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug")。  
  
-   按下 **F5**。  
  
 如果您使用建立報表但是未部署報表的專案組態，則在目前組態之 **StartItem** 屬性中所指定的報表，會在另一個預覽視窗中開啟。 預覽視窗顯示報表的方式和功能都與 [預覽] 模式相同。  
  
> [!NOTE]  
>  在偵錯報表之前，您必須設定一個啟動項目。 例如，如果您執行偵錯模式，瀏覽器會開啟主要報表伺服器頁面，而不是預覽模式的報表。 若要設定啟動項目，請在方案總管中以滑鼠右鍵按一下報表專案，再按一下 [屬性]，然後在 [StartItem] 中選取要顯示的報表名稱。  
  
 如果您想要預覽並非專案之啟動項目的特定報表，請選取建立報表但未部署報表的組態 (例如 DebugLocal 組態)，以滑鼠右鍵按一下報表，然後按一下 [執行]。 您必須選擇並未部署報表的組態；否則，報表將會發行至報表伺服器，而非在本機的預覽視窗中顯示。  
  
## <a name="publishing-to-a-test-server"></a>發行至測試伺服器  
 您也可以將報表發行至測試伺服器、瀏覽至報表並預覽，來測試報表。 將報表發行至測試伺服器與發行至實際伺服器相同。 如需發行報表的詳細資訊，請參閱 [將報表發行至報表伺服器](../../reporting-services/reports/publishing-reports-to-a-report-server.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [發行報表](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  

