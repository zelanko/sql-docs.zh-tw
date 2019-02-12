---
title: Analysis Services MDX 查詢設計工具使用者介面 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
helpviewer_keywords:
- query designers, Analysis Services
ms.assetid: 7e288eee-2d37-485e-a6a0-dbba5e041e26
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0c43e1d35b390a85a6e8951e182ce5408c7dd60c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017869"
---
# <a name="analysis-services-mdx-query-designer-user-interface-report-builder"></a>Analysis Services MDX 查詢設計工具使用者介面 (報表產生器)
  Report Builder 提供了圖形化查詢設計工具，可用來建立適用於 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源的多維度運算式 (MDX) 查詢。 MDX 圖形化查詢設計工具有兩種模式：設計模式和查詢模式。 每一種模式都會提供 [中繼資料] 窗格，您可以在這個窗格中，從選取的 Cube 中拖曳成員，以建立 MDX 查詢，在處理報表時擷取資料。  
  
> [!IMPORTANT]  
>  當使用者建立與執行查詢時，可以存取資料來源。 您應該授與資料來源的最小權限，例如唯讀權限。  
  
 下列幾節會針對圖形化查詢設計工具的各種模式，描述其中的工具列按鈕和查詢設計工具窗格。  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>設計模式中的圖形化 MDX 查詢設計工具  
 當您為報表資料集編輯 MDX 查詢時，圖形化 MDX 查詢設計工具會在 [設計] 模式下開啟。  
  
 下圖會標示出設計模式的窗格。  
  
 ![Analysis Services MDX 查詢設計工具，設計檢視](../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查詢設計工具，設計檢視")  
  
 下表列出此模式下的窗格：  
  
|窗格|函數|  
|----------|--------------|  
|[Select Cube (選取 Cube)] 按鈕 (**...**)|顯示目前選取的 Cube。|  
|[中繼資料] 窗格|顯示在選取的 Cube 上定義之量值、關鍵效能指標 (KPI) 和維度的階層式清單。|  
|[導出成員] 窗格|顯示目前已定義，可在查詢中使用的導出成員。|  
|[篩選] 窗格|用來選擇維度和相關階層，以便篩選來源端的資料和限制傳回給報表的資料。|  
|[資料] 窗格|在您從 [中繼資料] 窗格和 [導出成員] 窗格中拖曳項目時，顯示結果集的資料行標題。 如果已選取 **[自動執行]** 按鈕，便會自動更新結果集。 .|  
  
 您可以將 [中繼資料] 窗格中的維度、量值和 KPI 以及 [導出成員] 窗格中的導出成員，拖曳至 [資料] 窗格中。 在 [篩選] 窗格中，則可以選取維度和相關階層，以及設定篩選運算式來限制查詢可使用的資料。 如果已選取工具列上的 [自動執行] (![自動執行查詢](../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢")) 切換按鈕，則每次您將中繼資料物件放到 [資料] 窗格中時，查詢設計工具便會執行查詢。 您可以使用工具列上的 [執行] (![執行查詢](../analysis-services/media/rsqdicon-run.gif "執行查詢")) 按鈕，以手動方式執行查詢。  
  
 當您在此模式下建立 MDX 查詢時，查詢中會自動包含下列其他屬性：  
  
 **成員屬性** ：MEMBER_CAPTION、MEMBER_UNIQUE_NAME  
  
 **資料格屬性** ：VALUE、BACK_COLOR、FORE_COLOR、FORMATTED_VALUE、FORMAT_STRING、FONT_NAME、FONT_SIZE、FONT_FLAGS  
  
 若要指定您自己的其他屬性，您必須在 [查詢] 模式下手動編輯 MDX 查詢。  
  
> [!NOTE]  
>  如需有關 MDX 的詳細資訊以及 MDX 查詢設計工具的一般資訊，請參閱《 [SQL Server 線上叢書](https://go.microsoft.com/fwlink/?linkid=98335)》中的＜MDX 查詢編輯器 (Analysis Services - 多維度資料)＞。 不過，如果是從 MDX 查詢顯示資料的報表，則您必須使用報表產生器隨附的 MDX 查詢設計工具來建立查詢。 不支援從檔案匯入 .mdx 查詢。  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>設計模式中的圖形化 MDX 查詢設計工具工具列  
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。 下表列出這些按鈕及其功能。  
  
|按鈕|描述|  
|------------|-----------------|  
|**當成文字編輯**|這種資料來源類型不啟用|  
|**匯入**|從檔案系統上的報表定義 (.rdl) 檔案匯入現有的查詢。|  
|![變更為 MDX 查詢檢視](../analysis-services/media/rsqdicon-commandtypemdx.gif "變更為 MDX 查詢檢視")|切換到命令類型 MDX。|  
|![重新整理結果資料](../analysis-services/media/rsqdicon-refresh.gif "重新整理結果資料")|重新整理資料來源中的中繼資料。|  
|![Add calculated member](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|顯示 **[導出成員產生器]** 對話方塊。|  
|![切換以顯示空的資料格](../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空的資料格")|在顯示或隱藏 [資料] 窗格中的空白資料格之間切換 (這相當於使用 MDX 中的 NON EMPTY 子句)。|  
|![自動執行查詢](../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢")|每次進行變更時，自動執行查詢並顯示結果。 結果會顯示在 [資料] 窗格中。|  
|![顯示彙總按鈕](../analysis-services/media/rsqdicon-showaggregations.gif "顯示彙總按鈕")|將彙總顯示在 [資料] 窗格中。|  
|![刪除](../analysis-services/media/rsqdicon-delete.gif "刪除")|從查詢中刪除 [資料] 窗格中選取的資料行。|  
|![[查詢參數] 對話方塊圖示](../analysis-services/media/iconqueryparameter.gif "[查詢參數] 對話方塊圖示")|顯示 **[查詢參數]** 對話方塊。 當您指定查詢參數的值時，將會自動建立同名的報表參數。 查詢參數的值會設定為參考此報表參數的運算式。|  
|![準備查詢按鈕](../analysis-services/media/rsqdicon-preparequery.gif "準備查詢按鈕")|準備查詢。|  
|![執行查詢](../analysis-services/media/rsqdicon-run.gif "執行查詢")|執行查詢並將結果顯示在 [資料] 窗格中。|  
|![取消查詢](../analysis-services/media/rsqdicon-cancel.gif "取消查詢")|取消查詢。|  
|![切換到設計模式](../analysis-services/media/rsqdicon-designmode.gif "切換到設計模式")|在「設計」模式與「查詢」模式之間切換。|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>查詢模式中的圖形化 MDX 查詢設計工具  
 若要將圖形化查詢設計工具變更為 **[查詢]** 模式，請按一下工具列上的 **[設計模式]** 按鈕。  
  
 下圖會標示出「查詢」模式中的窗格。  
  
 ![Analysis Services MDX 查詢設計工具，查詢檢視](../analysis-services/media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX 查詢設計工具，查詢檢視")  
  
 下表列出此模式下的窗格：  
  
|窗格|函數|  
|----------|--------------|  
|[Select Cube (選取 Cube)] 按鈕 (**...**)|顯示目前選取的 Cube。|  
|[中繼資料/函數/範本] 窗格|顯示在選取的 Cube 上定義之量值、KPI 和維度的階層式清單。|  
|[查詢] 窗格|顯示查詢文字。|  
|結果窗格|顯示執行查詢的結果。|  
  
 [中繼資料] 窗格會顯示 **[中繼資料]**、 **[函數]** 和 **[範本]** 的索引標籤。 從 **[中繼資料]** 索引標籤中，可以將維度、階層、KPI 和量值拖曳至 [MDX 查詢] 窗格中。 從 **[函數]** 索引標籤中，可以將函數拖曳至 [MDX 查詢] 窗格中。 從 **[範本]** 索引標籤中，可以將 MDX 範本加入至 [MDX 查詢] 窗格中。 當您執行查詢時，[結果] 窗格會顯示 MDX 查詢的結果。  
  
 您可以擴充在 [設計] 模式下產生的預設 MDX 查詢，以包含其他成員屬性和資料格屬性。 當您執行查詢時，這些值不會出現在結果集中。 但是，這些值會隨資料集欄位集合傳回，而且您可以在報表中使用這些值。  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>查詢模式中的圖形化查詢設計工具工具列  
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。  
  
 「設計」模式與「查詢」模式的工具列按鈕完全相同，唯一不同的是在「查詢」模式中未啟用下列按鈕：  
  
-   **當成文字編輯**  
  
-   **加入導出成員** (![Add calculated member](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **顯示空的資料格** (![切換以顯示空的資料格](../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空的資料格"))  
  
-   **自動執行** (![自動執行查詢](../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢"))  
  
-   **顯示彙總** (![顯示彙總按鈕](../analysis-services/media/rsqdicon-showaggregations.gif "顯示彙總按鈕"))  
  
## <a name="see-also"></a>另請參閱  
 [查詢設計工具 &#40;報表產生器&#41;](../../2014/reporting-services/query-designers-report-builder.md)  
  
  
