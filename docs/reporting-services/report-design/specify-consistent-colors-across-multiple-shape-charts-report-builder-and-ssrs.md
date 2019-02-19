---
title: 指定多個形狀圖報表產生器-在 SSRS 中一致的色彩 |Microsoft 文件
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 38ff22fcfdb291c2ac3924985949142006eff812
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292186"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>跨多個形狀圖指定一致的色彩 (報表產生器及 SSRS)
  在分頁報表的非形狀圖上，您可以根據圖表中的數列索引， [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 從調色盤選取新的色彩。 例如，圖表上的第一個數列將會對應到調色盤中的第一個色彩。 不過，對於形狀圖來說，這個行為是不同的。 在形狀圖上，調色盤中的每個色彩都會對應到資料集中的資料點。 例如，資料點 1 對應到調色盤中的第一個色彩，資料點 2 對應到調色盤中的第二個色彩等等。  
  
 如果資料點沒有值，則不會顯示在形狀圖上。 也就是說，資料點會略過而不顯示任何色彩。 例如，如果點 2 的值為零，點 1 將會對應到調色盤中的第一個色彩，而點 3 將會對應到調色盤中的第二個色彩。 這個方法相當實用，因為不需要繪製空點時，圓形圖之資料集中的空點不一定要使用調色盤色彩。  
  
 副作用是，在報表中顯示多個圓形圖時，圓形圖可能會針對具有相同類別目錄群組的資料點顯示不同的色彩。 若要解決這個問題，您需要定義對應到類別目錄群組的個別色彩，而不是個別的資料值。 做法取決於形狀圖是否為資料表或矩陣中的走勢圖，或它們是否為報表本身中的形狀圖。  
  
 圖例會連接到數列，因此，您針對數列指定的任何色彩都會自動顯示在圖例上。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>若要在資料表或矩陣中跨多個走勢圖形狀圖指定一致的色彩  
  
1.  按一下圖表，即可顯示 [圖表資料] 窗格。  
  
2.  在 [類別目錄群組] 區域中，以滑鼠右鍵按一下某個類別目錄，然後按一下 [類別目錄群組屬性]。  
  
3.  在 [一般] 索引標籤的 [將群組同步處理於] 方塊中，按一下您要同步處理其色彩之類別目錄的名稱，然後按一下 [確定]。  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>若要跨多個形狀圖指定一致的色彩  
  
1.  以滑鼠右鍵按一下報表主體的外面，然後選取 [報表屬性]。  
  
2.  在 [程式碼] 中，將下列程式碼輸入到文字方塊中。  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  您需要將 "Color1" 字串取代成您自己的色彩。 您可以使用具名色彩 (例如 "Red")，或者您可以使用代表色彩的六位數十六進位值 (例如 "#FFFFFF" 代表黑色)。 如果您已經定義三個以上的色彩，您將需要擴充色彩的陣列，讓陣列中的色彩數目符合形狀圖中的點數。 您可以指定包含具名色彩或色彩十六進位表示法之字串值的逗號分隔清單，以便將新的色彩加入到陣列中。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  以滑鼠右鍵按一下形狀圖，並選取 [數列屬性]。  
  
5.  在 [填滿] 中，按一下 [運算式]\(*fx*) 按鈕來編輯 [色彩] 屬性的運算式。  
  
6.  輸入下列運算式，其中 "MyCategoryField" 是顯示在 [類別目錄群組] 區域中的欄位：  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [將斜面、浮凸與紋理樣式加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [將空點加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [形狀圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [走勢圖和資料橫條 &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
