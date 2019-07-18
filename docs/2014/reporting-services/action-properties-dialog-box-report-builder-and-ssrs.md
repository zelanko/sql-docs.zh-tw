---
title: 動作屬性對話方塊 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3d6069d5720121b02c627528ec772cb61ddb0a10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110074"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>動作屬性對話方塊 (報表產生器及 SSRS)
  **[動作]** 對話方塊可用於啟用支援連結之圖表、量測計與地圖元素的超連結選項。 定義動作，讓使用者可以按一下報表與 URL 的連結，便連結至相同報表伺服器或與報表伺服器整合之 SharePoint 網站上的不同報表，或連結至相同報表中的不同位置。  
  
## <a name="options"></a>選項。  
 **啟用為動作**  
 選取一個選項來指示使用者按一下項目時所執行的動作。  
  
 **無**  
 請選擇這個選項來指出項目沒有動作。  
  
 **移至報表**  
 選擇此選項即可建立位於報表伺服器之鑽研報表的連結。 當您選取 **[移至報表]** 時會出現下面其他選項。  
  
 **指定報表**  
 輸入或選取您要當做鑽研報表使用之報表的名稱。 鑽研報表必須位於與此報表相同的報表伺服器上。  
  
 對於發行到設定為原生模式之報表伺服器的報表，請使用不含副檔名的完整或相對路徑。 如果此報表與目前的報表在相同資料夾中，則只使用報表名稱。 如果報表位於相同報表伺服器上的不同資料夾中，請使用相對路徑或完整路徑。 相對路徑會從目前的資料夾開始，並將資料夾階層上移，例如，../Folder2/Report1。 完整路徑則是從 /，也又是主資料夾開始。 例如，/Reports/Report1。  
  
 對於發行到設定為 SharePoint 整合模式之報表伺服器的報表，請使用包含副檔名 (.rdl) 的完整 URL。 例如 http:// *\<//<sharepoint 伺服器名稱 > /\<站台 >*  /documents/report1.rdl。 不支援相對路徑。  
  
 如需詳細資訊，請參閱 msdn.microsoft.com 之[報表產生器文件](https://go.microsoft.com/fwlink/?LinkId=154494)中的[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 **使用這些參數執行報表**  
 加入參數清單，以傳遞至鑽研報表。 參數名稱必須符合針對目標報表定義的參數。 使用 **[加入]** 和 **[刪除]** 按鈕來加入和移除參數，並使用向上與向下箭頭來排列參數清單的順序。  
  
 **[加入]**  
 加入新的參數，以傳遞至鑽研報表。  
  
 **刪除**  
 刪除鑽研報表的參數。  
  
 **向上箭頭**  
 將清單中的參數向上移動。  
  
 **向下箭頭**  
 將清單中的參數向下移動。  
  
 **名稱**  
 輸入鑽研報表中定義之參數名稱的文字。  
  
 **值**  
 在鑽研報表中，為具名參數輸入或選取要傳遞的值。 請按一下 **運算式** (*fx*) 按鈕來編輯運算式。  
  
 **Omit**  
 選取此選項以防止參數執行。 根據預設，不會勾選也不會啟用此核取方塊。 若要選取此核取方塊，按一下 [運算式]  (*fx*) 按鈕，然後輸入 **True** 或建立一個運算式。 當您按一下 **[運算式]** 對話方塊中的 **[確定]** 時，就會選取此核取方塊。  
  
 **移至書籤**  
 選擇此選項即可在目前的報表中，定義書籤的連結。 當您選取 **[移至書籤]** 時會出現下面其他選項。  
  
 **選取書籤**  
 請輸入或選取書籤識別碼，這是當使用者按一下連結時要跳至的目的地。 按一下 [運算式] (**fx**) 按鈕以變更運算式。 書籤識別碼可以是靜態識別碼或者會評估為書籤識別碼的運算式。 此運算式可包含具有書籤識別碼的欄位。  
  
 若要連結到書籤，您必須先設定報表項目的 [書籤] 屬性。 若要設定 [書籤] 屬性，請選取報表項目，然後在 [屬性] 窗格中輸入書籤識別碼的值或運算式，例如 SalesChart 或 5TopSales。  
  
 **移至 URL**  
 請選擇這個選項來定義通往網頁的連結。 請輸入或選取網頁的 URL，或會評估結果為網頁 URL 的運算式。 按一下 [運算式]  (*fx*) 按鈕以變更運算式。 這個運算式可以包括含有 URL 的欄位。 當您選取 **[移至 URL]** 時會出現下面其他選項。  
  
 **選取 URL**  
 輸入或輸入項目的 URL。 對於發行到設定為原生模式之報表伺服器的項目，請使用完整或相對路徑， 例如 http:// *\<伺服器名稱 >* images/image1.jpg。 對於發行到報表伺服器設定為 SharePoint 整合模式的項目，則使用完整的 URL (例如 http:// *\<//<sharepoint 伺服器名稱 > /\<站台 >*  /記載/影像 /image1.jpg)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [新增子報表和參數 &#40;報表產生器及 SSRS&#41;](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  
