---
title: 新增資料來源檢視的預測 （中繼資料採礦教學課程） |Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823128"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>加入預測用的資料來源檢視 (中繼資料採礦教學課程)
  在這項工作中，您將新增資料來源檢視，以便用於預測狀況。 預測模型的資料，必須包含可用來識別時間序列步驟的資料行。 如果您計畫分析多個資料序列，所有序列必須在同一個日期或時間步驟結束。  
  
### <a name="to-add-a-data-source-view"></a>若要加入資料來源檢視  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下**資料來源檢視**，然後選取**新的資料來源檢視**。  
  
2.  在 [歡迎使用資料來源檢視精靈] 頁面上，按一下 [下一步]。  
  
3.  在  **Zdroj Dat**頁面的 **關聯式資料來源**，選取[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]資料來源。 按一下 [下一步] 。  
  
    > [!NOTE]  
    >  如果您沒有此資料來源，您可以找到建立資料來源中的步驟[83c8-9df5dddfeb9c"&gt;basic Data Mining Tutorial&lt](../../2014/tutorials/basic-data-mining-tutorial.md)。  
  
4.  在 **選取資料表和檢視**頁面上，選取 vTimeSeries (dbo) 資料表，然後按一下向右箭號，將它新增至資料來源檢視。  
  
5.  按一下 [下一步] 。  
  
6.  在 [**完成精靈]** 頁面上，依預設名稱的資料來源檢視是[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 將名稱變更為**SalesByRegion**，然後按一下**完成**。  
  
     資料來源檢視設計師會開啟並**SalesByRegion**資料來源檢視會出現。  
  
## <a name="working-with-the-data-source-view"></a>使用資料來源檢視  
 資料來源檢視建立完成之後，可以用下列方法探索資料：  
  
-   以滑鼠右鍵按一下 vTimeSeries 資料表在設計師中，然後選取**瀏覽資料**以在方格中開啟選取的資料表。  
  
-   按一下 **取樣選項**，然後使用**資料瀏覽選項**對話方塊來變更取樣方法。 按一下 **重新整理**載入新的選項設定為使用的資料表中的資料。 例如，您可以指定輸出在範例中，或選擇 前 n 個資料列的資料列的數目。  
  
-   以滑鼠右鍵按一下 vTimeSeries 資料表，然後選取**屬性**將新的名稱指派至資料表。 您還可以從資料來源檢視中選取個別資料行，並且修改資料行的屬性。  
  
-   按一下資料來源檢視設計區域中的任意位置建立新查詢並且指派該查詢的名稱、建立資料表之間的關聯性，或是變更設計區域的配置。  
  
-   以滑鼠右鍵按一下資料表，然後選取**新增具名計算**建立衍生的資料行，包括彙總。 您也可以從這個檢視的資料來源加入新資料表和檢視。  
  
 在下一項工作中，您將瀏覽時間序列資料，並判斷最適合做為時間序列識別碼的資料行。 您還會學習如何處理時間序列資料中的間距。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [了解需求時間序列模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
