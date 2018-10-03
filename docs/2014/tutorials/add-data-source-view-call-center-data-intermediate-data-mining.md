---
title: 新增資料來源檢視的撥接中心資料 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f212c6436af0e35c7cfaceadf8c519765d0a07a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171941"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>加入用於撥接中心資料的資料來源檢視 (中繼資料採礦教學課程)
  在這項工作中，您將加入資料來源檢視，用來存取撥接中心資料。 相同的資料將用於建立用來進行探索的初步類神經網路模型，以及用於提出建議的羅吉斯迴歸模型。  
  
 您也將會使用資料來源檢視設計工具，為週中的日加入一個資料行。 因為雖然來源資料依日期追蹤撥接中心的資料，但是您根據經驗得知，依據當天是工作日或週末，在通話量和服務品質方面有重複的模式。  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-add-a-data-source-view"></a>若要加入資料來源檢視  
  
1.  中**方案總管**，以滑鼠右鍵按一下**資料來源檢視**，然後選取**新增資料來源檢視**。  
  
     此時會開啟資料來源檢視精靈。  
  
2.  在 [歡迎使用資料來源檢視精靈] 頁面上，按一下 [下一步]。  
  
3.  在  **Zdroj Dat**頁面的 **關聯式資料來源**，選取[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]資料來源。 如果您沒有此資料來源，請參閱[83c8-9df5dddfeb9c"&gt;basic Data Mining Tutorial&lt](../../2014/tutorials/basic-data-mining-tutorial.md)。 按 [下一步] 。  
  
4.  在 **選取資料表和檢視**頁面上，選取下列資料表，然後按一下向右箭號，將它新增至資料來源檢視：  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  按 [下一步] 。  
  
6.  在 [**完成精靈]** 頁面上，依預設名稱的資料來源檢視是[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 將名稱變更為**CallCenter**，然後按一下**完成**。  
  
     資料來源檢視設計師會開啟並顯示**撥接中心**資料來源檢視。  
  
7.  在 [資料來源檢視] 窗格中，以滑鼠右鍵按一下並選取**加入/移除資料表**。 選取的資料表中， **DimDate**然後按一下**確定**。  
  
     關聯性應該會自動加入之間`DateKey`每個資料表中的資料行。 您將使用此關聯性來取得資料行**EnglishDayNameOfWeek**，從**DimDate**資料表，並在您的模型中使用它。  
  
8.  在 資料來源檢視設計工具中，以滑鼠右鍵按一下資料表中， **FactCallCenter**，然後選取**新增具名計算**。  
  
     在 **建立具名計算**對話方塊方塊中，輸入下列值：  
  
    |||  
    |-|-|  
    |**資料行名稱**|DayOfWeek|  
    |**說明**|從 DimDate 資料表取得週中的日|  
    |**運算式**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     若要確認運算式建立資料您需要請以滑鼠右鍵按一下資料表**FactCallCenter**，然後選取**瀏覽資料**。  
  
9. 花一分鐘檢閱可用的資料，以便了解資料在資料採礦中的用法：  
  
|資料行名稱|包含|  
|-----------------|--------------|  
|FactCallCenterID|當資料匯入資料倉儲時建立的任意索引鍵。<br /><br /> 此資料行會識別唯一記錄，應該做為資料採礦模型的案例索引鍵。|  
|DateKey|撥接中心作業的日期，以整數表示。 資料倉儲中通常使用整數日期索引鍵，但是如果您要依日期值進行分組，可能想要取得日期/時間格式的日期。<br /><br /> 請注意，日期不是唯一的，因為廠商會在作業的每一天，為每個排班提供一個個別的報表。|  
|WageType|表示該日期為工作日、週末或假日。<br /><br /> 很可能已有不同的客戶服務品質的工作日與週末讓您將使用此資料行做為輸入。|  
|Shift|表示記錄電話當時的排班。 此撥接中心將工作日分成四個排班：AM、PM1、PM2，以及 Midnight。<br /><br /> 排班可能對客戶服務品質造成影響，因此您將它做為輸入。|  
|LevelOneOperators|表示待命的一級操作員數目。<br /><br /> 撥接中心員工從一級開始，因此這些員工資歷較淺。|  
|LevelTwoOperators|表示待命的二級操作員數目。<br /><br /> 員工必須記錄特定的服務時數才能限定為二級操作員。|  
|TotalOperators|排班期間出現的操作員總數。|  
|Calls|排班期間接到的電話通數。|  
|AutomaticResponses|完全由自動化電話處理 (互動式語音應答，也就是 IVR) 所處理的電話通數。|  
|Orders|來自電話的訂單數目。|  
|IssuesRaised|由電話產生、需要後續追蹤的問題數目。|  
|AverageTimePerIssue|回應來電所需的平均時間。|  
|ServiceGrade|表示一般服務品質，計量以*放棄率*整個排班。 放棄率越高，客戶越可能不滿意，而且可能會遺失潛在的訂單。|  
  
 請注意，資料會包含為基礎的單一日期資料行的四個不同資料行： `WageType`， **DayOfWeek**， `Shift`，和`DateKey`。 通常在資料採礦中，最好不要使用多個衍生自相同資料的資料行，因為值的相互關聯性太強，可能會遮蔽其他模式。  
  
 不過，我們不會使用`DateKey`模型中因為它包含太多唯一值。 之間沒有直接關聯性`Shift`並**DayOfWeek**，以及`WageType`並**DayOfWeek**只部分相關。 如果您對共線性有顧慮，可以使用所有可用的資料行建立結構，然後忽略各模型中不同的資料行並測試效果。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立類神經網路結構和模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
