---
title: "使用 Reporting Services 中的 KPI | Microsoft Docs"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# 使用 Reporting Services 中的 KPI
關鍵效能指標 (KPI) 是用以傳達達成目標之進度量的視覺提示。  關鍵效能指標是對於團隊、管理人員及企業而言非常重要，此指標使其可快速評估對可測量目標所做的進度。   
  
使用 SQL Server 2016 Reporting Services 中的 KPI，您就能輕鬆地以視覺化方式回答下列問題︰  
  
-   我現在正處於哪個階段前後？  
  
-   我之前或之後還有多遠的距離？  
  
-   我已完成的最低程度是什麼？  
  
## 建立資料集  
KPI 只會使用共用資料集的第一列資料。 請確定您想要使用的資料位於第一列。 若要建立共用資料集，您可以使用報表產生器或 SQL Server Data Tools。  
  
> **注意**︰資料集不需要位於與 KPI 相同的資料夾。  
  
## KPI 的位置  
  
您可以在報表伺服器的任何資料夾中建立 KPI。  建立 KPI 之前，您會想要考慮要將它放在哪裡才是正確的位置。 您會想將它放在使用者可以看見的資料夾中，同時也與其周圍的其他報告和 KPI 相關。  
  
## 加入 KPI  
  
決定您的 KPI 的位置之後，請移至該資料夾，然後從上方功能表選取 [新增] > [KPI]。  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
這會為您顯示 [新增 KPI] 畫面。  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
您可以指派靜態值，或使用共用資料集的資料。 當您建立新的 KPI 時，即會填入一組隨機的手動資料。  
  
|欄位|說明|  
|---|---|  
|值格式|  用來變更顯示值的格式。|   
|Value|針對 KPI 顯示的值。|  
|目標|用來與數值比較且以差異百分比​​顯示。|  
|狀態|用於判斷 KPI 圖格色彩的數值。 有效值為 1 (綠色)、 0 (琥珀色) 和 -1 (紅色)。|  
|趨勢集|用於圖表視覺效果且以逗點分隔的數值。 這也可以設定為資料集的資料行，其值代表趨勢。|  
  
> **警告**︰雖然您可以在設計階段使用 [狀態] 欄位的文字值，但如果會重新整理資料集，您就應該使用數值。 如果您使用文字值 (而非數字) 重新整理資料集，它可能會損毀您伺服器上的 KPI。  
  
> **注意**：[值]、[目標] 和 [狀態] 欄位只可以從資料集結果的第一列中選擇值。 不過，[趨勢集] 欄位可以選擇哪些資料行會反映趨勢。  
  
您可以執行下列步驟來使用共用資料集的資料。  
  
1.  將欄位下拉式清單方塊從 [手動設定] 或 [未設定] 變更為 [資料集欄位]。  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  選取資料方塊中的**省略符號 (...)**。 這將會顯示 [挑選資料集] 畫面。  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  選取包含您想要顯示之資料的資料集。  
  
4.  選擇您想要使用的欄位。 選取 [確定]。  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  變更 [值格式] 以符合您的值格式。 在此範例中，值是一種貨幣。  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  選取 [套用]。  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## 移除 KPI  
  
若要移除 KPI，您可以執行下列動作。  
  
1.  選取您想要移除之 KPI 的**省略符號 (...)**。 選取 [管理]。  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  選取 [刪除]。 在確認對話方塊中，再次選取 [刪除]。  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## 重新整理 KPI  
  
若要重新整理 KPI，您必須設定共用資料集的**快取重新整理計劃** 。 您目前不能從入口網站設定快取重新整理計劃。 您必須移至舊的報表管理員來執行這項操作。   
  
這將會逐步解說如何使用一些基本設定來設定快取重新整理計劃。 如需快取重新整理計劃的詳細資訊，請參閱[快取重新整理選項 (報表管理員)](Cache%20Refresh%20Options%20(Report%20Manager).xml)。  
  
1.  開啟報表管理員，然後找出您想要設定快取重新整理計劃屬性的共用資料集。   
  
2.  將滑鼠停留在報表或共用資料集上方，然後選取下拉式箭號。  
  
3.  從下拉式清單中選取 [管理]。 [一般屬性] 頁面隨即開啟。  
  
4.  選取 [快取重新整理選項] 索引標籤。  
  
5.  若要建立新的快取計劃，請選取 [新增快取重新整理計劃]。  
  
    ![rsRefreshKPI1](../reporting-services/media/rsrefreshkpi1.png)  
  
6.  您將會收到一則訊息，詢問您是否要使用預設選項來啟用這個項目的快取。 選取 [確定]。  
  
    > **注意**：您必須啟用並啟動 SQL Server Agent 服務來建立快取重新整理計劃。  
  
7.  您可以選擇特定的排程，或選取共用的排程 (如果有的話)。  
  
8.  執行快取重新整理計劃的排程時，將會更新 KPI 的值。  
  
    ![rsRefreshKPI2](../reporting-services/media/rsrefreshkpi2.png)  
  
## 另請參閱  
  
- [入口網站 (SSRS 原生模式)](../reporting-services/web-portal-ssrs-native-mode.md)  
  
- [快取重新整理選項 (報表管理員)](Cache%20Refresh%20Options%20(Report%20Manager).xml)  
  
    
  
  
  
