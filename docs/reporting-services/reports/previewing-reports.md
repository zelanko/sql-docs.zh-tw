---
title: 預覽報表
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 82559832d11d9461665e89963026a267d9f0554c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267493"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>在 SQL Server Reporting Services (SSRS) 中預覽報表

  設計 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表時，在尚未發佈至生產環境之前，您可能會想要先檢視該報表。 您可以利用數種方式進行檢視：在報表設計師中切換到 [預覽] 模式、使用報表設計師中的預覽視窗，以及在測試環境中將報表發行至報表伺服器。  
  
> [!NOTE]  
> 預覽報表時，報表的資料會快取至本機電腦上的檔案。 當您再次預覽同一份報表時 (使用相同的查詢、參數和認證)，報表設計師會擷取快取複本，而非重新執行查詢。 資料檔案儲存為 *\<reportname>* .rdl.data 與報表定義檔案相同的目錄中。 您關閉報表設計師時，不會刪除此檔案。  
  
## <a name="preview-mode"></a>預覽模式

 您可以預覽報表在報表設計師中的，依序按一下![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview")。 這會在本機執行報表，使用與報表伺服器相同的報表處理與轉譯功能。 顯示的報表是互動式影像；您可以選取參數、按一下連結、檢視文件引導模式，以及展開和摺疊報表的隱藏區域。 您也可以將報表匯出至任何已安裝的轉譯格式。  
  
## <a name="standalone-preview"></a>獨立預覽

 另一個預覽報表的方式是在偵錯組態下執行報表專案，例如，偵錯您撰寫的自訂組件。 報表會在預設瀏覽器中開啟。 有三種方法可以執行專案：  
  
- 在 [偵錯]  功能表中，按一下 [開始偵錯]  。  
  
- 依序按一下**啟動**按鈕[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)][標準] 工具列![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug")。  
  
- 按下 **F5**。  
  
 如果您使用建立報表但是未部署報表的專案組態，則在目前組態之 **StartItem** 屬性中所指定的報表，會在另一個預覽視窗中開啟。 預覽視窗顯示報表的方式和功能都與 [預覽] 模式相同。  
  
> [!NOTE]  
> 在偵錯報表之前，您必須設定一個啟動項目。 例如，如果您執行偵錯模式，瀏覽器會開啟主要報表伺服器頁面，而不是預覽模式的報表。 若要設定啟動項目，請在方案總管中以滑鼠右鍵按一下報表專案，再按一下 [屬性]  ，然後在 [StartItem]  中選取要顯示的報表名稱。  
  
 如果您想要預覽並非專案之啟動項目的特定報表，請選取建立報表但未部署報表的組態 (例如 DebugLocal 組態)，以滑鼠右鍵按一下報表，然後按一下 [執行]  。 您必須選擇並未部署報表的組態；否則，報表將會發行至報表伺服器，而非在本機的預覽視窗中顯示。  
  
## <a name="publish-to-a-test-server"></a>發佈至測試伺服器

 您也可以將報表發行至測試伺服器、瀏覽至報表並預覽，來測試報表。 將報表發行至測試伺服器與發行至實際伺服器相同。 如需發行報表的詳細資訊，請參閱 [將報表發行至報表伺服器](../../reporting-services/reports/publishing-reports-to-a-report-server.md)。  
  
## <a name="next-steps"></a>後續步驟

 - [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)
 - [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)
 - [發佈報表](https://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)
 - [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)