---
title: SAP NetWeaver BI 查詢設計工具使用者介面 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10014"
helpviewer_keywords:
- query designers, SAP
ms.assetid: 8edda06d-1608-498b-bd50-10905e54f6ce
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 34248f660d31d6993ce21a0bcced0e0857b685cb
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029129"
---
# <a name="sap-netweaver-bi-query-designer-user-interface-report-builder"></a>SAP NetWeaver BI 查詢設計工具使用者介面 (報表產生器)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了圖形化查詢設計工具，可用來建立適用於 SAP NetWeaver® Business Intelligence 資料來源的多維度運算式 (MDX) 查詢。 MDX 圖形化查詢設計工具有兩種模式：設計模式和查詢模式。 每一種模式都會提供 [中繼資料] 窗格，您可以在這個窗格中，從資料來源上定義的 InfoCube、MultiProvider 或 Web 查詢中拖曳成員，從而建立 MDX 查詢，在處理報表時擷取資料。  
  
> [!IMPORTANT]  
>  當使用者建立與執行查詢時，可以存取資料來源。 您應該授與資料來源的最小權限，例如唯讀權限。  
  
 本節會針對圖形化查詢設計工具的各種模式，描述其中的工具列按鈕和查詢設計工具窗格。  
  
## <a name="graphical-query-designer-in-design-mode"></a>設計模式中的圖形化查詢設計工具  
 當您編輯的資料集查詢使用了 [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)] 資料來源時，圖形化查詢設計工具會在設計模式下開啟。  
  
 ![在設計模式下使用 MDX 的查詢設計工具](media/rsqd-dssapbw-mdx-designmode.gif "在設計模式下使用 MDX 的查詢設計工具")  
  
 下表列出此模式下的窗格。  
  
|窗格|函數|  
|----------|--------------|  
|[選取 Cube] 按鈕|顯示目前選取的 InfoCube、MultiProvider 或 Web 查詢。|  
|[中繼資料] 窗格|顯示 InfoCube、MultiProvider 和查詢的階層式清單。 在資料來源建立的查詢可能會顯示在對應的 Cube 底下。|  
|[導出成員] 窗格|顯示目前已定義，可在查詢中使用的導出成員。|  
|[資料] 窗格|顯示執行查詢的結果。|  
  
 您可以將 [中繼資料] 窗格中的維度和重要數據以及 [導出成員] 窗格中的導出成員，拖曳至 [資料] 窗格中。 如果工具列上的 **[自動執行]** 切換按鈕為開啟狀態，則每次您將物件放到 [資料] 窗格中時，查詢設計工具便會執行查詢。 如果 **[自動執行]** 為關閉狀態，則當您對 [資料] 窗格進行變更時，查詢設計工具不會執行查詢。 您可以使用工具列上的 **[執行]** 按鈕，以手動方式執行查詢。  
  
### <a name="toolbar-for-the-graphical-query-designer-in-design-mode-toolbar"></a>設計模式中的圖形化查詢設計工具工具列  
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。 下表描述這些按鈕及其功能。  
  
|按鈕|描述|  
|------------|-----------------|  
|**當成文字編輯**|在以文字為基礎的查詢設計工具和圖形化查詢設計工具之間切換。 無法用於這種資料來源類型。|  
|**匯入**|從檔案系統上的報表定義 (.rdl) 檔案匯入現有的查詢。|  
|![重新整理資料集欄位](media/rsqdicon-refreshfields.gif "重新整理資料集欄位")|重新整理資料來源中的中繼資料。|  
|![Add calculated member](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|顯示 **[導出成員產生器]** 對話方塊。|  
|![切換以顯示空的資料格](../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空的資料格")|在顯示或隱藏 [資料] 窗格中的空白資料格之間切換 (這相當於使用 MDX 中的 NON EMPTY 子句)。|  
|![自動執行查詢](../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢")|每次進行變更 (例如刪除 [資料] 窗格中的資料行) 時自動執行查詢並顯示結果。 結果會顯示在 [資料] 窗格中。|  
|![刪除](../analysis-services/media/rsqdicon-delete.gif "刪除")|從查詢中刪除 [資料] 窗格中選取的資料行。|  
|![[查詢參數] 對話方塊圖示](../analysis-services/media/iconqueryparameter.gif "[查詢參數] 對話方塊圖示")|顯示 **[變數]** 對話方塊。 只有當選取的 Cube 是查詢 Cube 時，才會啟用這個按鈕 (因為只有查詢 Cube 才支援變數)。 當您指派預設值給變數時，就會建立對應的報表參數。|  
|![執行查詢](../analysis-services/media/rsqdicon-run.gif "執行查詢")|執行查詢並將結果顯示在 [資料] 窗格中。|  
|![取消查詢](../analysis-services/media/rsqdicon-cancel.gif "取消查詢")|取消查詢。|  
|![切換到設計模式](../analysis-services/media/rsqdicon-designmode.gif "切換到設計模式")|在「設計」模式與「查詢」模式之間切換。|  
  
## <a name="graphical-query-designer-in-query-mode"></a>查詢模式中的圖形化查詢設計工具  
 若要將圖形化查詢設計工具變更為「查詢」模式，請按一下工具列上的 **[設計模式]** 切換按鈕。  
  
 下圖會指出查詢設計工具在「查詢」模式中的各個部分。  
  
 ![查詢檢視中的 SAP BW MDX 查詢設計工具](media/rsqd-dssapbw-mdx-querymode.gif "查詢檢視中的 SAP BW MDX 查詢設計工具")  
  
 下表會描述各個窗格的功能。  
  
|窗格|函數|  
|----------|--------------|  
|[選取 Cube] 按鈕|顯示目前選取的 InfoCube、MultiProvider 或其他 Cube。|  
|[中繼資料/函數] 窗格|顯示索引標籤式的視窗，列出可用來建立查詢文字的可用中繼資料或函數清單。|  
|[變數] 窗格|顯示目前已定義，可在查詢中使用的變數。|  
|[查詢] 窗格|顯示目前的查詢文字。|  
|結果窗格|顯示查詢的結果。|  
  
 在 [中繼資料] 窗格中，您可以將 **[中繼資料]** 索引標籤上的重要數據和維度拖曳至 [MDX 查詢] 窗格中；中繼資料的技術名稱會插入於游標所在的位置。 您也可以將 **[函數]** 索引標籤上的函數拖曳至 [MDX 查詢] 窗格中。 當您執行查詢時，[結果] 窗格便會顯示目前 MDX 查詢的結果。  
  
 如果您選取的 Cube 是 Web 查詢，則會提示您為現有的變數設定靜態預設值， 然後您就可以將變數拖曳至 [MDX 查詢] 窗格中。  
  
 [中繼資料] 窗格和 [變數] 窗格會顯示易記名稱。 當您將物件放到 [MDX 查詢] 窗格中時，就可以看到資料來源所需的技術名稱已輸入到 MDX 查詢中。  
  
### <a name="toolbar-for-the-graphical-query-designer-in-query-mode"></a>查詢模式中的圖形化查詢設計工具工具列  
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。 「設計」模式與「查詢」模式的工具列按鈕完全相同，唯一不同的是在「查詢」模式中未啟用下列按鈕：  
  
-   **當成文字編輯**  
  
-   **加入導出成員** (![Add calculated member](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **顯示空的資料格** (![切換以顯示空的資料格](../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空的資料格"))  
  
-   **自動執行** (![自動執行查詢](../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢"))  
  
-   **刪除** (![刪除](../analysis-services/media/rsqdicon-delete.gif "刪除"))  
  
## <a name="see-also"></a>另請參閱  
 [查詢設計工具 &#40;報表產生器&#41;](../../2014/reporting-services/query-designers-report-builder.md)  
  
  
