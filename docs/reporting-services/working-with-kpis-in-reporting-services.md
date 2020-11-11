---
title: 使用 Reporting Services 中的 KPI | Microsoft Docs
description: 了解如何透過使用 SQL Server Reporting Services 中的 KPI，輕鬆測量狀態和效能。
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: e661fee4e9b5afe5f78cae444ff8d6574a536bb9
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243777"
---
# <a name="working-with-kpis-in-reporting-services"></a>使用 Reporting Services 中的 KPI

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

*關鍵效能指標 (KPI)* 是用以傳達達成目標之進度量的視覺提示。  關鍵效能指標是對於團隊、管理人員及企業而言非常重要，此指標使其可快速評估對可測量目標所做的進度。
  
使用 SQL Server Reporting Services 中的 KPI，您就能輕鬆地以視覺化方式回答下列問題︰  
  
- 我現在正處於哪個階段前後？  
  
- 我之前或之後還有多遠的距離？  
  
- 我已完成的最小數量為何？  

> [!NOTE]
> 只有在 SSRS 入口網站的 Enterprise (Developer) 版本中才能存取 KPI。

## <a name="creating-a-dataset"></a>建立資料集

KPI 只會使用共用資料集的第一列資料。 請確定您想要使用的資料位於第一列。 若要建立共用資料集，您可以使用報表產生器或 SQL Server Data Tools。  
  
> **注意** ：資料集不需要位於與 KPI 相同的資料夾。  
  
## <a name="placement-of-kpis"></a>KPI 的位置  
  
您可以在報表伺服器的任何資料夾中建立 KPI。  建立 KPI 之前，您會想要考慮要將它放在哪裡才是正確的位置。 您可以將它放在使用者可以看見的資料夾中，同時也與其周圍的其他報告和 KPI 相關。  
## <a name="adding-a-kpi"></a>加入 KPI
  
決定您 KPI 的位置之後，請移至該資料夾，然後從上方功能表選取 [新增] > [KPI]。  
  
![顯示 [新增] 下拉式清單的螢幕擷取畫面，其中已標註 [KPI] 選項。](../reporting-services/media/rscreatekpi1.png)  
  
這會為您顯示 [新增 KPI] 畫面。  
  
![顯示 [新增 KPI] 畫面的螢幕擷取畫面。](../reporting-services/media/rscreatekpi2.png)  
  
您可以指派靜態值，或使用共用資料集的資料。 當您建立新的 KPI 時，即會填入一組隨機的手動資料。  
  
| 欄位 | 說明 |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 值格式 | 用來變更顯示值的格式。 |
| 值 | 針對 KPI 顯示的值。 |
| 目標 | 用來與數值比較且以差異百分比​​顯示。 |
| 狀態 | 用於判斷 KPI 圖格色彩的數值。 有效值為 1 (綠色)、 0 (琥珀色) 和 -1 (紅色)。 |
| 趨勢集 | 用於圖表視覺效果且以逗點分隔的數值。 這也可以設定為資料集的資料行，其值代表趨勢。 |
| 相關內容 | 能夠設定鑽研連結。 此連結可以是在入口網站上所發佈行動報表或自訂的 URL。 |
  
> **警告** ︰雖然您可以在設計階段使用 [狀態] 欄位的文字值，但如果會重新整理資料集，您就應該使用數值。 如果您使用文字值 (而非數字) 重新整理資料集，它可能會損毀您伺服器上的 KPI。  
>
> **注意** ：[值]、[目標] 和 [狀態] 欄位只可以從資料集結果的第一列中選擇值。 不過，[趨勢集] 欄位可以選擇哪些資料行會反映趨勢。  
  
您可以執行下列步驟來使用共用資料集的資料。
  
1. 將欄位下拉式清單方塊從 [手動設定] 或 [未設定] 變更為 [資料集欄位]。  
  
    ![顯示 [值] 選項已設定為 [資料集欄位] 且 [挑選資料集欄位] 已設定為 [未設定] 的螢幕擷取畫面。](../reporting-services/media/rscreatekpi3.png)  
  
2. 選取資料方塊中的 **省略符號 (...)** 。 這將會顯示 [挑選資料集] 畫面。  
  
    ![[挑選資料集] 區段的螢幕擷取畫面，其中已選取 [Finance_KPI] 選項。](../reporting-services/media/rscreatekpi4.png)  
  
3. 選取包含您想要顯示之資料的資料集。  
  
4. 選擇您想要使用的欄位。 選取 [確定]。  
  
    ![顯示 [從 Finance_KPI 挑選欄位] 區段的螢幕擷取畫面，其中已選取 [Sum_Amount] 選項。](../reporting-services/media/rscreatekpi5.png)  
  
5. 變更 [值格式] 以符合您的值格式。 在此範例中，值是一種貨幣。  
  
    ![KPI 預覽的螢幕擷取畫面，其中顯示 [值格式] 選項已設定為 [貨幣]。](../reporting-services/media/rscreatekpi6.png)  
  
6. 選取 [套用]。  
  
    ![KPI 的螢幕擷取畫面，其中顯示 [資料集] 具有兩個項目。](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>設定相關內容

當選擇 [行動報表] 時，您可以在對話方塊中選擇目的地。

   ![顯示 [相關內容] 選項已設定為 [行動報表] 且 [選擇行動報表] 選項已設定為 [未設定] 的螢幕擷取畫面。](media/rscreatekpi-related-content-mobile-report.png)

當您現在按一下入口網站中的 KPI 時，行動報表的縮圖會顯示在 [相關內容] 下拉式清單下。 按一下此縮圖可直接巡覽至這份報表。

您也可以指定自訂的 URL。 這項工作可以是任何形式：網站、SharePoint 網站、SSRS 報表的 URL (這可讓您沿著硬式編碼的參數傳遞)。

![顯示 [相關內容] 選項已設定為 [自訂 URL] 且 [輸入 URL] 選項已設定為 [http://] 的螢幕擷取畫面。](media/rscreatekpi-related-content-custom-url.png)

當您現在按一下 KPI 時，URL 會顯示在相關內容下。

您只能新增一份行動報表或一個自訂 URL。
  
## <a name="removing-a-kpi"></a>移除 KPI  
  
若要移除 KPI，您可以執行下列步驟。
  
1. 選取您想要移除之 KPI 的 **省略符號 (...)** 。 選取 [管理]。  
  
    ![已選取 KPI 省略符號選項並標註 [管理] 選項的螢幕擷取畫面。](../reporting-services/media/rsremovekpi1.png)  
  
2. 選取 [刪除] 。 在確認對話方塊中，再次選取 [刪除]。  
  
    ![[刪除] 選項的螢幕擷取畫面。](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>重新整理 KPI  
  
若要重新整理 KPI，您必須設定共用資料集的快取。 如需快取重新整理計劃的詳細資訊，請參閱[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)。  
  
## <a name="next-steps"></a>後續步驟
  
[入口網站](../reporting-services/web-portal-ssrs-native-mode.md)  
[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
