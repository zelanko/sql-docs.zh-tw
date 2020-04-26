---
title: 加入用於預測的資料來源視圖（中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f60ea2b2a642cf9435ed8366c42e43abb927e426
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62823128"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>加入預測用的資料來源檢視 (中繼資料採礦教學課程)
  在這項工作中，您將新增資料來源檢視，以便用於預測狀況。 預測模型的資料，必須包含可用來識別時間序列步驟的資料行。 如果您計畫分析多個資料序列，所有序列必須在同一個日期或時間步驟結束。  
  
### <a name="to-add-a-data-source-view"></a>若要加入資料來源檢視  
  
1.  在方案總管中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
2.  在 [歡迎使用資料來源檢視精靈]**** 頁面上，按 [下一步]****。  
  
3.  在 [**選取資料來源**] 頁面的 [**關聯式資料來源**] 底下， [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]選取資料來源。 按 [下一步]  。  
  
    > [!NOTE]  
    >  如果您沒有此資料來源，您可以在[基本資料採礦教學](../../2014/tutorials/basic-data-mining-tutorial.md)課程中找到建立資料來源的步驟。  
  
4.  在 [**選取資料表和 Views]** 頁面上，選取資料表 [vTimeSeries （Dbo）]，然後按一下向右箭號，將它加入至 [資料來源] 視圖。  
  
5.  按 [下一步]  。  
  
6.  在 [**正在完成嚮導]** 頁面上，預設會將 [資料來源[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]] 視圖命名為。 將名稱變更為**salesbyregion.dsv**，然後按一下 **[完成]**。  
  
     [資料來源視圖設計工具] 隨即開啟，並顯示 [ **salesbyregion.dsv** ] 資料來源視圖。  
  
## <a name="working-with-the-data-source-view"></a>使用資料來源檢視  
 資料來源檢視建立完成之後，可以用下列方法探索資料：  
  
-   以滑鼠右鍵按一下設計工具中的資料表 vTimeSeries，然後選取 [**流覽資料**]，在方格中開啟選取的資料表。  
  
-   按一下 [**取樣選項**]，然後使用 [**資料流覽選項**] 對話方塊來變更取樣方法。 按一下 **[** 重新整理]，使用新的選項設定載入資料表中的資料。 例如，您可以指定要在取樣中輸出的資料列數目，或選擇前 n 個數據列。  
  
-   以滑鼠右鍵按一下資料表 vTimeSeries，然後選取 [**屬性**]，將新名稱指派給資料表。 您還可以從資料來源檢視中選取個別資料行，並且修改資料行的屬性。  
  
-   按一下資料來源檢視設計區域中的任意位置建立新查詢並且指派該查詢的名稱、建立資料表之間的關聯性，或是變更設計區域的配置。  
  
-   以滑鼠右鍵按一下資料表，然後選取 [新增] [**命名計算**] 以建立衍生的資料行，包括匯總。 您也可以從這個檢視的資料來源加入新資料表和檢視。  
  
 在下一項工作中，您將瀏覽時間序列資料，並判斷最適合做為時間序列識別碼的資料行。 您還會學習如何處理時間序列資料中的間距。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [瞭解時間序列模型的需求 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
