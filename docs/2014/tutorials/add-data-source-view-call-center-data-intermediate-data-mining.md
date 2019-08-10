---
title: 加入撥打電話中心資料的資料來源視圖 (中繼資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 04f930c42b0e41a9f10b35d10295a38e8dac7490
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888680"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>加入用於撥接中心資料的資料來源檢視 (中繼資料採礦教學課程)
  在這項工作中，您將加入資料來源檢視，用來存取撥接中心資料。 相同的資料將用於建立用來進行探索的初步類神經網路模型，以及用於提出建議的羅吉斯迴歸模型。  
  
 您也將會使用資料來源檢視設計工具，為週中的日加入一個資料行。 因為雖然來源資料依日期追蹤撥接中心的資料，但是您根據經驗得知，依據當天是工作日或週末，在通話量和服務品質方面有重複的模式。  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-add-a-data-source-view"></a>若要加入資料來源檢視  
  
1.  在**方案總管**中, 以滑鼠右鍵按一下 [**資料來源視圖**], 然後選取 [**新增資料來源視圖**]。  
  
     此時會開啟資料來源檢視精靈。  
  
2.  在 [歡迎使用資料來源檢視精靈] 頁面上，按一下 [下一步]。  
  
3.  在 [**選取資料來源**] 頁面的 [**關聯式資料來源**] 底下[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] , 選取資料來源。 如果您沒有此資料來源, 請參閱[基本資料採礦教學](../../2014/tutorials/basic-data-mining-tutorial.md)課程。 按一下 [下一步]。  
  
4.  在 [**選取資料表和資料檢視]** 頁面上, 選取下列資料表, 然後按一下向右箭號, 將它加入至資料來源視圖:  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  按一下 [下一步]。  
  
6.  在 [**正在完成嚮導]** 頁面上, 預設會將 [資料來源[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]] 視圖命名為。 將名稱變更為**CallCenter**, 然後按一下 **[完成]** 。  
  
     [資料來源視圖設計工具] 隨即開啟, 以顯示 [ **CallCenter** ] 資料來源視圖。  
  
7.  以滑鼠右鍵按一下 [資料來源] 視圖窗格內, 然後選取 [**新增/移除資料表]** 。 選取資料表**DimDate** , 然後按一下 **[確定]** 。  
  
     應該在每個資料表的`DateKey`資料行之間自動加入關聯性。 您將使用此關聯性從**DimDate**資料表取得**EnglishDayNameOfWeek**資料行, 並在您的模型中使用它。  
  
8.  在 [資料來源視圖設計工具] 中, 以滑鼠右鍵按一下資料表**FactCallCenter**, 然後選取 [新增] [**命名計算**]。  
  
     在 [**建立命名計算**] 對話方塊中, 輸入下列值:  
  
    |||  
    |-|-|  
    |**資料行名稱**|DayOfWeek|  
    |**描述**|從 DimDate 資料表取得週中的日|  
    |**運算式**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     若要確認運算式是否會建立您所需的資料, 請以滑鼠右鍵按一下資料表**FactCallCenter**, 然後選取 [**流覽資料**]。  
  
9. 花一分鐘檢閱可用的資料，以便了解資料在資料採礦中的用法：  
  
|資料行名稱|包含|  
|-----------------|--------------|  
|FactCallCenterID|當資料匯入資料倉儲時建立的任意索引鍵。<br /><br /> 此資料行會識別唯一記錄，應該做為資料採礦模型的案例索引鍵。|  
|DateKey|撥接中心作業的日期，以整數表示。 資料倉儲中通常使用整數日期索引鍵，但是如果您要依日期值進行分組，可能想要取得日期/時間格式的日期。<br /><br /> 請注意，日期不是唯一的，因為廠商會在作業的每一天，為每個排班提供一個個別的報表。|  
|WageType|表示該日期為工作日、週末或假日。<br /><br /> 客戶服務在週末與工作日的品質可能有所差異, 因此您將使用此資料行做為輸入。|  
|Shift|表示記錄電話當時的排班。 此話務中心會將工作日分成四個移位:AM、PM1、PM2 和午夜。<br /><br /> 排班可能對客戶服務品質造成影響，因此您將它做為輸入。|  
|LevelOneOperators|表示待命的一級操作員數目。<br /><br /> 撥接中心員工從一級開始，因此這些員工資歷較淺。|  
|LevelTwoOperators|表示待命的二級操作員數目。<br /><br /> 員工必須記錄特定的服務時數才能限定為二級操作員。|  
|TotalOperators|排班期間出現的操作員總數。|  
|Calls|排班期間接到的電話通數。|  
|AutomaticResponses|完全由自動化電話處理 (互動式語音應答，也就是 IVR) 所處理的電話通數。|  
|Orders|來自電話的訂單數目。|  
|IssuesRaised|由電話產生、需要後續追蹤的問題數目。|  
|AverageTimePerIssue|回應來電所需的平均時間。|  
|ServiceGrade|指出一般服務品質的度量, 以整個排班的*放棄速率*來測量。 放棄率越高，客戶越可能不滿意，而且可能會遺失潛在的訂單。|  
  
 請注意, 資料包含四個以單一日期資料行為基礎的不同資料`WageType`行:、 `Shift` **DayOfWeek**、 `DateKey`和。 通常在資料採礦中，最好不要使用多個衍生自相同資料的資料行，因為值的相互關聯性太強，可能會遮蔽其他模式。  
  
 不過, 我們不會在`DateKey`模型中使用, 因為它包含太多的唯一值。 和`Shift` **DayOfWeek 之間**沒有直接的關聯性, 而且 和DayOfWeek只有部分`WageType`相關。 如果您對共線性有顧慮，可以使用所有可用的資料行建立結構，然後忽略各模型中不同的資料行並測試效果。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立類神經網路結構和模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
