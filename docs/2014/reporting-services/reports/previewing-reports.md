---
title: 預覽報表
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 21928cd6637815000983e8a0fe05aa4e77d1c216
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412976"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>在 SQL Server Reporting Services (SSRS) 中預覽報表

  設計報表時，在尚未發行至實際環境之前，您可能會想要先檢視該報表。 您可以利用數種方式進行檢視：在報表設計師中切換到 [預覽] 模式、使用報表設計師中的預覽視窗，以及在測試環境中將報表發行至報表伺服器。  
  
> [!NOTE]  
> 預覽報表時，報表的資料會快取至本機電腦上的檔案。 當您再次預覽同一份報表時 (使用相同的查詢、參數和認證)，報表設計師會擷取快取複本，而非重新執行查詢。 資料檔案儲存為 *\<reportname>* .rdl.data 與報表定義檔案相同的目錄中。 您關閉報表設計師時，不會刪除此檔案。  
  
## <a name="preview-mode"></a>預覽模式

 您可以預覽報表在報表設計師中的，依序按一下**預覽**。 這會在本機執行報表，使用與報表伺服器相同的報表處理與轉譯功能。 顯示的報表是互動式影像；您可以選取參數、按一下連結、檢視文件引導模式，以及展開和摺疊報表的隱藏區域。 您也可以將報表匯出至任何已安裝的轉譯格式。  
  
## <a name="standalone-preview"></a>獨立預覽

 另一個預覽報表的方式是在偵錯組態下執行報表專案，例如，偵錯您撰寫的自訂組件。 有三種方法可以執行專案：  
  
- 依序按一下**開始**上**偵錯**功能表。  
  
- 依序按一下**開始**按鈕[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]標準 工具列。  
  
- 可按下 F5。  
  
 如果您使用建立報表但是未部署報表的專案組態，則在目前組態之 `StartItem` 屬性中所指定的報表，會在另一個預覽視窗中開啟。 預覽視窗顯示報表的方式和功能都與 [預覽] 模式相同。  
  
> [!NOTE]  
> 在偵錯報表之前，您必須設定一個啟動項目。 若要設定啟動項目，在 [方案總管] 中，以滑鼠右鍵按一下報表專案，請按一下**屬性**，然後在`StartItem`，選取要顯示報表的名稱。  
  
 如果您想要預覽並非專案之啟動項目的特定報表，請選取建立報表但未部署報表的組態 (例如 DebugLocal 組態)，以滑鼠右鍵按一下報表，然後按一下 [執行]  。 您必須選擇並未部署報表的組態；否則，報表將會發行至報表伺服器，而非在本機的預覽視窗中顯示。  
  
## <a name="print-preview"></a>預覽列印

 當您第一次在 [預覽] 模式或預覽視窗中檢視報表時，報表的檢視類似於 HTML 轉譯延伸模組所產生的報表。 這個預覽並不是 HTML，不過報表的配置及分頁與 HTML 的輸出相似。  
  
 您可以切換到預覽列印模式，以變更檢視來顯示列印的報表。 按一下預覽工具列上的 **[預覽列印]** 按鈕。 所顯示的報表就如同在實際頁面上所看到的。 這個檢視與影像和 PDF 轉譯延伸模組所產生的輸出類似。 預覽列印並不是影像或 PDF 檔案，不過報表的配置及分頁與這些格式的輸出相似。  
  
## <a name="publish-to-a-test-server"></a>發佈至測試伺服器

 您也可以將報表發行至測試伺服器來測試報表。 將報表發行至測試伺服器與發行至實際伺服器相同。 如需發行報表的詳細資訊，請參閱 [將報表發行至報表伺服器](publishing-reports-to-a-report-server.md)。  
  
## <a name="next-steps"></a>後續步驟

 - [列印報表 &#40;報表產生器及 SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)
 - [列印報表 &#40;報表產生器及 SSRS&#41;](../report-builder/print-a-report-report-builder-and-ssrs.md)
 - [發佈報表](../publish-reports.md)
 - [將自訂組件與報表搭配使用](../custom-assemblies/using-custom-assemblies-with-reports.md)