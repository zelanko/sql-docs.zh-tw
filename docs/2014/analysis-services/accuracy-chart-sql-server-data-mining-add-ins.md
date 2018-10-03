---
title: 精確度圖表 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- mining models, validating
- mining models, charting
- lift chart
- mining models, testing
- lift [data mining]
ms.assetid: 303973b4-71c0-4cfc-b7bc-92218b52509d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 328ce6c6474beb68d14edd26779d868142a29fd0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136794"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>精確度圖表 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的精確度圖表按鈕](media/dmc-accchart.gif "資料採礦功能區中的 [精確度圖表] 按鈕")  
  
 精確度圖表可讓您將模型套用到新的資料集，然後評估模型執行的妥善程度。 此精靈所建立的精確度圖表*增益圖*，這是一種經常用來測量資料採礦模型的精確度的圖表。 這種類型的精確度圖表會顯示與隨機預測和 100% 預測均為精確的理想案例相較之下，使用指定的資料採礦模型所取得之改進的圖形表示。 您可以在單一圖表中比較多個模型。  
  
## <a name="example"></a>範例  
 請考量 Adventure Works Cycles 的行銷部門所要建立的鎖定郵寄活動案例。 根據以往的活動，他們知道通常可以收到百分之 10 的回應率。 他們在資料庫的資料表中儲存了一份 10,000 位潛在客戶的清單。 根據一般的回應率，他們預期有 1,000 位客戶會回應。  
  
 但是因為他們只能負擔將廣告郵寄給 5,000 名客戶，因此行銷部門使用採礦模型針對 5,000 最可能回應的客戶。  
  
 如果公司隨機選取 5,000 位客戶，則預期只會收到 500 個正面回應，因為鎖定的客戶中通常只有百分之 10 會回應。 此狀況就是增益圖中的隨機線條代表的意義。  
  
 不過，如果行銷部門使用採礦模型來鎖定郵寄，而且該模型是完美的，公司便會預期在將廣告郵寄到模型所建議的 1,000 位潛在客戶時，可收到 1,000 位的回應。 在增益圖中以理想線條代表此狀況。  
  
## <a name="using-the-accuracy-chart-wizard"></a>使用精確度圖表精靈  
 若要建立精確度圖表，您必須參考現有的資料採礦結構。 只要預測的是相同的事情，您就可以根據該結構，測量多個模型的精確度。  
  
 如果不確定可以使用哪些結構，您可以瀏覽伺服器。 如需詳細資訊，請參閱 < [Excel 中的 瀏覽模型&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。  
  
#### <a name="to-create-an-accuracy-chart"></a>建立精確度圖表  
  
1.  按一下 **資料採礦用戶端**功能區。  
  
2.  在 **精確度和驗證**群組中，按一下**精確度圖表**。  
  
3.  在 **選取結構或模型**對話方塊方塊中，選擇您想要評估的模型。 按 [下一步] 。  
  
    > [!NOTE]  
    >  您必須選擇緊密符合您所要測試之資料的模型。  
  
4.  在 **預測及要預測的值指定資料行**對話方塊方塊中，選擇您想要預測的資料行和目標值，如果適用的話。 按 [下一步] 。  
  
     例如，在以上的範例中，您可能選擇模型化客戶回應的資料行，並將目標值指定為 "Probably Will Buy"。  
  
    > [!NOTE]  
    >  您無法預測連續的值； 但是，您可以將值分在離散範圍來離散化資料行。 您必須先進行這項處理，然後才能建立資料採礦模型。  
  
5.  在 **選取來源資料**對話方塊方塊中，指定會傳遞通過模型以便建立預測的資料來源。  
  
6.  如果您使用外部的資料，而不會儲存在模型中，測試資料來源**指定的關聯性**對話方塊中，對應中新的來源資料的資料行的資料行使用資料採礦模型中。  
  
     如果資料行名稱相似，精靈便會自動加以對應。 雖然輸入資料中的某些資料行可能與分析無關而且可以忽略，但是還需要某些資料行，資料採礦模型才能處理輸入。 這類資料行可能包含交易識別碼、目標值或用於預測的資料行。 如果您無法對應所需的資料行，此精靈將會提供一則警告訊息。  
  
7.  按一下 **[完成]**。  
  
     精靈會建立報表，其中包含增益圖和基礎資料。  
  
### <a name="requirements"></a>需求  
 如果您是在預測離散值，便必須選取您所要預測的目標值。 例如，如果您的資料被分類成回應 "Yes: Buy" 為 1，回應 "No: Do Not Buy" 為 2，您就必須將 1 或 2 指定為預測值。 不過，如果您要預測值的範圍，便只能在同時比較兩個值。 例如，如果您要預測高於 5 的分數，便必須重新標籤您的來源資料，並建立將結果分割為兩組的新模型：高於 5 的分數和低於 5 的分數。 然後您便可以比較這兩個群組的精確度。  
  
## <a name="understanding-accuracy"></a>了解精確度  
 您可以建立兩種類型的圖表，其中一個指定可預測資料行的狀態，另一個不指定狀態。  
  
 如果您指定可預測資料行的狀態，圖表的 x 軸代表用來比較預測之測試資料集的百分比。 圖表的 y 軸代表預測做為指定狀態之值的百分比。  
  
 如果您不指定可預測資料行的狀態，該圖表就會針對所有可能的預測，顯示圖表的精確度。  
  
 如需有關增益圖如何運作，以及如何根據隨機和理想預測線來計算精確度的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中的＜增益圖＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [驗證模型及使用模型進行預測&#40;資料採礦適用於 Excel 的增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
