---
title: 工具列 （瀏覽器索引標籤，Cube 設計工具） (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c20904d56add8256de37351c1435d06f8f526277
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023197"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>工具列 (瀏覽器索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  在 Cube 設計師中使用 [工具列] 內的功能執行常見的作業，同時設計或瀏覽 Cube 或其物件，或者建立 MDX 查詢。 設計階段與查詢檢視通用的作業包括設定使用者內容、處理物件，以及設定預設語言。  
  
 下表列出 [工具列] 按鈕及其功能。  
  
|按鈕|描述|  
|------------|-----------------|  
|**當成文字編輯**|這種資料來源類型不啟用|  
|**匯入**|從檔案系統上的報表定義 (.rdl) 檔案匯入現有的查詢。|  
|![變更為 MDX 查詢檢視](media/rsqdicon-commandtypemdx.gif "變更為 MDX 查詢檢視")|切換到命令類型 MDX。|  
|![重新整理結果資料](media/rsqdicon-refresh.gif "重新整理結果資料")|重新整理資料來源中的中繼資料。|  
|![加入導出的成員](media/rsqdicon-addcalculatedmember.gif "加入導出的成員")|顯示 **[導出成員產生器]** 對話方塊。|  
|![切換以顯示空的資料格](media/rsqdicon-showemptycells.gif "切換以顯示空的資料格")|在顯示或隱藏 [資料] 窗格中的空白資料格之間切換 (這相當於使用 MDX 中的 NON EMPTY 子句)。|  
|![自動執行查詢](media/rsqdicon-autoexecute.gif "自動執行查詢")|每次進行變更時，自動執行查詢並顯示結果。 結果會顯示在 [資料] 窗格中。|  
|![顯示彙總按鈕](media/rsqdicon-showaggregations.gif "顯示彙總按鈕")|將彙總顯示在 [資料] 窗格中。|  
|![刪除](media/rsqdicon-delete.gif "刪除")|從查詢中刪除 [資料] 窗格中選取的資料行。|  
|![[查詢參數] 對話方塊圖示](media/iconqueryparameter.gif "[查詢參數] 對話方塊圖示")|顯示 **[查詢參數]** 對話方塊。 當您指定查詢參數的值時，將會自動建立同名的參數。|  
|![準備查詢按鈕](media/rsqdicon-preparequery.gif "準備查詢按鈕")|準備查詢。|  
|![執行查詢](media/rsqdicon-run.gif "執行查詢")|執行查詢並將結果顯示在 [資料] 窗格中。|  
|![取消查詢](media/rsqdicon-cancel.gif "取消查詢")|取消查詢。|  
|![切換到設計模式](media/rsqdicon-designmode.gif "切換到設計模式")|在「設計」模式與「查詢」模式之間切換。|  
  
 一般而言，[設計模式] 與 [查詢模式] 的工具列按鈕相同。 不過，系統未針對 [查詢模式] 啟用下列按鈕：  
  
-   **當成文字編輯**  
  
-   **加入導出成員**(![加入導出的成員](media/rsqdicon-addcalculatedmember.gif "加入導出的成員"))  
  
-   **顯示空的資料格** (![切換以顯示空的資料格](media/rsqdicon-showemptycells.gif "切換以顯示空的資料格"))  
  
-   **自動執行** (![自動執行查詢](media/rsqdicon-autoexecute.gif "自動執行查詢"))  
  
-   **顯示彙總** (![顯示彙總按鈕](media/rsqdicon-showaggregations.gif "顯示彙總按鈕"))  
  
## <a name="options"></a>選項。  
  
|選項|描述|  
|------------|-----------------|  
|**處理**|按一下以顯示 **[處理]** 對話方塊，並處理 Cube。 如需 [處理] 對話方塊的詳細資訊，請參閱[處理對話方塊 &#40;Analysis Services - 多維度資料&#41;](process-dialog-box-analysis-services-multidimensional-data.md)。|  
|**變更使用者**|按一下即可顯示 [安全性內容] 對話方塊，並變更用於 [瀏覽器] 索引標籤上的使用者和角色。如需 [安全性內容] 對話方塊的詳細資訊，請參閱[安全性內容對話方塊 &#40;Analysis Services - 多維度資料&#41;](security-context-dialog-box-analysis-services-multidimensional-data.md)。|  
|**重新連線**|如果 [瀏覽器] 索引標籤的工作階段因連接遺失或逾時而中斷連接，按一下即可將 [計算] 索引標籤重新連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體和包含 Cube 的資料庫。|  
|**[重新整理]**|按一下即可重新整理 [中繼資料] 和 [報表] 窗格。|  
|**遞增排序**|按一下即可依 [語言] 中所指定語言的遞增順序，來排序 [報表] 窗格中選取之資料列的同層級。<br /><br /> **注意**：只有選取 [報表] 窗格中的資料格時，才會啟用此選項。|  
|**遞減排序**|按一下即可依 [語言] 中所指定語言的遞減順序，來排序 [報表] 窗格中選取之資料列的同層級。<br /><br /> 注意：只有選取 [報表] 窗格中的資料格時，才會啟用此選項。|  
|**自動篩選**|按一下即可自動篩選 [結果] 窗格中的結果。|  
|**顯示只上/下**|選取一個值或百分比，以根據選取的量值，在 [報表] 窗格中只顯示最上層或最下層的資料格數目或資料格的百分比。<br /><br /> 如需這個選項的詳細資訊，請參閱 [TopCount &#40;MDX&#41;](/sql/mdx/topcount-mdx)、[TopPercent &#40;MDX&#41;](/sql/mdx/toppercent-mdx)、[BottomCount &#40;MDX&#41;](/sql/mdx/bottomcount-mdx) 和 [BottomPercent &#40;MDX&#41;](/sql/mdx/bottompercent-mdx)。|  
|**小計**|按一下即可顯示小計。|  
|**所有項目的總計**|按一下即可顯示 [報表] 窗格中之所有成員的總計。|  
|**顯示空白資料格**|按一下即可顯示 [報表] 窗格中之空的資料格。|  
|**清除結果**|按一下即可清除 [報表] 窗格中的結果。|  
|**命令和選項**|按一下即可顯示 [命令與選項] 對話方塊，並編輯 [報表] 窗格中之 Microsoft Office 11.0 樞紐分析表控制項的進階屬性。 如需 [命令與選項] 對話方塊的詳細資訊，請參閱 Microsoft Office 文件。|  
|**檢視方塊**|選取用來檢視 [中繼資料] 和 [報表] 窗格中之資料與中繼資料的檢視方塊。<br /><br /> 若要檢視 Cube 而不使用檢視方塊，請選取 Cube 名稱。|  
|**語言**|選取用來檢視 [中繼資料] 和 [報表] 窗格中之資料與中繼資料的語言。<br /><br /> 若要使用預設語言檢視 Cube，請選取 [預設值]。|  
  
  
