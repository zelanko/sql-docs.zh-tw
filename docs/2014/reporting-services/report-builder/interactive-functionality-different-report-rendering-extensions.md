---
title: 不同報表轉譯延伸模組 （報表產生器及 SSRS） 的互動式功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c66e8e8ce302044cac8caf488ca27a0c0c07651e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107803"
---
# <a name="interactive-functionality-for-different-report-rendering-extensions-report-builder-and-ssrs"></a>不同報表轉譯延伸模組的互動式功能 (報表產生器及 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供互動式報表功能，讓您能夠在執行階段使用報表。 並非所有報表轉譯格式都支援互動式功能的完整範圍。 您可以利用下表來了解每個互動式功能在特定格式中的運作方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="interactive-features-in-different-output-formats"></a>不同輸出格式中的互動式功能  
 轉譯為 XML、CSV 或影像格式的報表不支援互動式功能。  
  
 您在報表管理員、SharePoint Web 組件或瀏覽器中檢視的報表會以 HTML 轉譯。 HTML 和 Windows Form 是唯一完全支援所有互動式功能的報表輸出格式。 替代的 HTML 格式 (例如：MHTML) 支援多種互動式功能。 如果存在 MHTML 例外狀況，下表會記載這些例外狀況。  
  
### <a name="document-maps"></a>文件引導模式  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|互動式文件引導模式提供階層式連結的導覽窗格，讓您用來導覽到不同的報表區段。|  
|PDF|PDF 會將文件引導模式轉譯成 [書籤] 窗格。 文件引導模式中的所有項目會在窗格中由上往下列出。 它包含連結的階層。 如果有指定頁面範圍，只有經過轉譯的書籤才存在於階層中。|  
|[匯出]|Excel 會將文件引導模式轉譯成活頁簿中的第一個工作表。 它包含連結的階層。 按一下文件引導模式中的連結時，會在個別的活頁簿中開啟適當的目標資料格。|  
|Word|Word 會將文件引導模式轉譯成 [目錄] 標籤。|  
|其他 (例如 TIFF、XML 和 CSV)|不適用於 MHTML、XML、CSV 或影像。|  
  
### <a name="drillthrough-links-to-other-reports"></a>其他報表的鑽研連結  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|使用者按一下報表中的資料值，即可檢視另一份報表中的相關資料。|  
|PDF|在 PDF 中則無法使用鑽研連結。 針對連結至其他頁面的 PDF 報表，請考慮使用超連結。|  
|[匯出]|鑽研連結是以 Excel 轉譯。<br /><br /> 連結變成指向鑽研連結所參考之報表的超連結。 按一下連結，即可在瀏覽器視窗中開啟報表。|  
|Word|鑽研連結是以 Word 轉譯。<br /><br /> 連結變成指向鑽研連結所參考之報表的超連結。 按一下連結，即可在瀏覽器視窗中開啟報表。|  
|其他|不適用於 XML、CSV 或影像。|  
  
### <a name="toggle-items-within-a-report"></a>在報表內切換項目  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|使用者按一下 [展開] 和 [摺疊] 圖示，即可檢視報表的各區段。|  
|PDF|報表伺服器會將目前報表的顯示或隱藏狀態匯出至 PDF。 不支援互動式切換|  
|[匯出]|可以切換的鑽研連結和項目會轉譯為 Excel 中可折疊的大綱。 您可以在 Excel 中展開及摺疊報表的各區段。 如需 Excel 規定限制的詳細資訊，請參閱[匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)。|  
|Word|報表伺服器會將目前報表的顯示或隱藏狀態匯出至 PDF。 不支援互動式切換|  
|其他|不適用於 MHTML、XML 或 CSV。 匯出到影像格式時，報表伺服器會將目前報表的顯示或隱藏狀態匯出至 PDF。 不支援互動式切換。|  
  
### <a name="interactive-sorting"></a>互動式排序  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|如果是表格式報表，使用者只要按一下資料行上的排序箭頭，即可變更資料的排序方式。|  
|PDF|不適用於 PDF。|  
|[匯出]|不適用於 Excel。|  
|Word|不適用於 Word。|  
|其他|不適用於 MHTML、XML、CSV 或影像。|  
  
### <a name="hyperlinks-to-external-web-content-or-images"></a>外部 Web 內容或影像的超連結  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|使用者按一下連結，即可在新的瀏覽器視窗中開啟外部網頁。|  
|PDF|PDF 轉譯延伸模組會轉譯超連結。 當使用者按下超連結時，連結的頁面會在瀏覽器中開啟。|  
|[匯出]|超連結是以 Excel 轉譯。|  
|Word|超連結是以 Word 轉譯。|  
|其他|超連結不適用於 MHTML、XML、CSV 或影像。<br /><br /> 如果是 MHTML 和影像，外部影像會轉譯為靜態圖片。|  
  
### <a name="bookmark-or-anchor"></a>書籤或錨點  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|使用者按一下連結，即可導覽到相同報表的另一個區段。|  
|PDF|不適用於 PDF。|  
|[匯出]|書籤是以 Excel 轉譯。<br /><br /> 書籤會變成指向報表項目名稱的超連結。|  
|Word|書籤是以 Word 轉譯。<br /><br /> 書籤會變成指向加上書籤之報表項目的超連結。 匯出報表時，僅能轉換 40 個字元的書籤或錨點名稱，這可能會導致書籤或錨點名稱重複。 空格會轉換成底線 (_)。|  
|其他|不適用於 XML、CSV 或影像。|  
  
### <a name="prompted-parameters-obtained-at-run-time"></a>在執行階段取得的提示參數  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|參數輸入區域會出現在報表頂端。 此區域是在瀏覽器中顯示報表時所用之 HTML 檢視器的一部分。|  
|PDF|報表伺服器會利用目前對報表有效的參數值，將報表匯出至 PDF。|  
|[匯出]|報表伺服器會利用目前對報表有效的參數值，將報表匯出至 Excel。|  
|Word|報表伺服器會利用目前對報表有效的參數值，將報表匯出至 Word。|  
|其他|報表伺服器會利用目前對報表有效的參數值，將報表匯出至其他格式。|  
  
### <a name="filters-applied-at-run-time"></a>在執行階段套用的篩選  
  
|匯出選項|支援資訊|  
|-------------------|-------------------------|  
|預覽/報表檢視器、HTML|執行階段會對使用者顯示篩選資料。|  
|PDF|報表伺服器會利用目前報表中的篩選資料，將報表匯出至 PDF。|  
|[匯出]|報表伺服器會利用目前報表中的篩選資料，將報表匯出至 Excel。|  
|Word|報表伺服器會利用目前報表中的篩選資料，將報表匯出至 Word。|  
|其他|報表伺服器會利用目前報表中的篩選資料，將報表匯出至其他格式。|  
  
## <a name="see-also"></a>另請參閱  
 [匯出報表&#40;報表產生器及 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](../report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
  
