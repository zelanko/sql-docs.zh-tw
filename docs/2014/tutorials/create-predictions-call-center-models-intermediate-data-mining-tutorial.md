---
title: 建立預測的撥接中心模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5be0cec7-f639-4eeb-835e-e3204ae619e9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30f24ab457669f572189d2eb13deca3f672f5e18
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025409"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>建立用於撥接中心模型的預測 (中繼資料採礦教學課程)
  現在您已經了解排班、操作員數目、電話，以及服務等級之間的互動關係，接著就可以準備建立一些用來進行商務分析和規劃的預測查詢。 您將先針對探勘模型建立一些預測，以測試一些假設。 接著您將使用羅吉斯迴歸模型建立大量預測。  
  
 本課程假設您已熟悉預測查詢的概念。  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>使用類神經網路模型建立預測  
 下列範例示範如何使用為了探索資料所建立的類神經網路模型進行單一預測。 單一預測可以讓您嘗試不同的值，是觀察在模型中會產生何種效果的好方法。 在這個案例中，您將預測如果有六個經驗豐富的操作員值班，大夜班 (未指定星期幾) 的服務等級將是哪個等級。  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>若要使用類神經網路模型建立單一查詢  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟包含您要使用之模型的方案。  
  
2.  在 [資料採礦設計師中，按一下**採礦模型預測**] 索引標籤。  
  
3.  在 **採礦模型**窗格中，按一下**選取模型**。  
  
4.  **選取採礦模型**對話方塊會顯示採礦結構的清單。 展開採礦結構，檢視與該結構相關聯之採礦模型的清單。  
  
5.  展開採礦結構 [撥接中心預設值]，然後選取類神經網路模型 [撥接中心 – LR]。  
  
6.  從 [採礦模型] 功能表中選取 [單一查詢]。  
  
     **單一查詢輸入**對話方塊隨即出現，其中資料行會對應到採礦模型中的資料行。  
  
7.  在 **單一查詢輸入** 對話方塊中，按一下 排班，資料列，然後按*午夜*。  
  
8.  按一下 Lvl 2 Operators，然後輸入資料列`6`。  
  
9. 在底部的一半**採礦模型預測**索引標籤上，按一下方格中的第一個資料列。  
  
10. 在 **來源**資料行中，按一下向下箭號，然後選取**預測函數**。 在 **欄位**欄中，選取**PredictHistogram**。  
  
     您可以自動使用此預測函數的引數清單會出現在**準則/引數** 方塊中。  
  
11. 從清單中的資料行拖曳 ServiceGrade 資料行**採礦模型**窗格，即可**準則/引數** 方塊中。  
  
     資料行的名稱會自動插入做為引數。 您可以選擇任何可預測的屬性資料行，將其拖曳至此文字方塊中。  
  
12. 按一下按鈕**切換到查詢結果檢視**，在預測查詢產生器的上方。  
  
 結果應該會包含每個服務等級在這些輸入條件下可能產生的預測值，以及每個預測的支援和機率。 您可以隨時返回設計檢視並變更輸入，或加入更多輸入。  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>使用羅吉斯迴歸模型建立預測  
 如果您已經知道與商務問題相關的屬性，則可以使用羅吉斯迴歸模型，預測變更某些屬性後所造成的效果。 羅吉斯迴歸是一種統計方式，通常用於根據獨立變數 (例如財務計分) 中的變更來進行預測，例如，根據客戶人口統計來預測客戶行為。  
  
 在此工作中，您將學習如何建立用於預測的資料來源，然後進行預測以協助回答數個商務問題。  
  
### <a name="generating-data-used-for-bulk-prediction"></a>產生用於大量預測的資料  
 您可以利用許多方式提供輸入資料：例如，您可以從試算表匯入人員雇用層級，然後在模型中執行該資料，以預測下個月的服務品質。  
  
 在這一課，您將使用資料來源檢視設計工具來建立具名查詢。 這個具名查詢是一個自訂 Transact-SQL 陳述式，可針對每個排班來計算排班操作員人數上限、接聽電話下限，以及所產生的平均問題數目。 然後您會將該資料聯結至採礦模型，進行有關一系列未來日期的預測。  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>若要產生用於大量預測查詢的輸入資料  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下**資料來源檢視**，然後選取**新的資料來源檢視**。  
  
2.  在 [資料來源檢視精靈] 中，選取[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]作為資料來源，然後按一下**下一步**。  
  
3.  在 [**選取資料表和檢視表**頁面上，按一下**下一步]** 但不選取任何資料表。  
  
4.  在 **完成精靈**頁面上，輸入名稱， `Shifts`。  
  
     這個名稱會顯示在 [方案總管] 中，做為資料來源檢視的名稱。  
  
5.  以滑鼠右鍵按一下空的設計窗格，然後選取**新的具名查詢**。  
  
6.  在 [**建立具名查詢**] 對話方塊中，如**名稱**，型別`Shifts for Call Center`。  
  
     這個名稱會顯示在 [資料來源檢視設計師] 中，但只會做為具名查詢的名稱。  
  
7.  將下列查詢陳述式貼到對話方塊下半部的 SQL 文字窗格中。  
  
    ```  
    SELECT DISTINCT WageType, Shift,   
    AVG(Orders) as AvgOrders, MIN(Orders) as MinOrders, MAX(Orders) as MaxOrders,  
    AVG(Calls) as AvgCalls, MIN(Calls) as MinCalls, MAX(Calls) as MaxCalls,  
    AVG(LevelTwoOperators) as AvgOperators, MIN(LevelTwoOperators) as MinOperators, MAX(LevelTwoOperators) as MaxOperators,  
    AVG(IssuesRaised) as AvgIssues, MIN(IssuesRaised) as MinIssues, MAX(IssuesRaised) as MaxIssues  
    FROM dbo.FactCallCenter  
    GROUP BY Shift, WageType  
    ```  
  
8.  在 設計 窗格中，以滑鼠右鍵按一下資料表 Shifts for Call Center，並選取**瀏覽資料**來預覽 T-SQL 查詢所傳回的資料。  
  
9. 以滑鼠右鍵按一下  索引標籤中， **Shifts.dsv (Design)，** ，然後按一下**儲存**以儲存新的資料來源檢視定義。  
  
### <a name="predicting-service-metrics-for-each-shift"></a>預測每個排班的服務標準  
 現在您已經為每個排班產生一些值，您將使用這些值做為您所建立之羅吉斯迴歸模型的輸入，以產生可用於商務計畫的一些預測。  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>若要使用新的 DSV 做為預測查詢的輸入  
  
1.  在 [資料採礦設計師中，按一下**採礦模型預測**] 索引標籤。  
  
2.  在 **採礦模型**窗格中，按一下**選取模型**，，然後選擇 撥接中心-LR，從可用模型的清單。  
  
3.  從**採礦模型**功能表上，清除選項**單一查詢**。 此時會出現一個警告，告知您將會失去單一查詢輸入。 按一下 [確定] 。  
  
     **單一查詢輸入** 對話方塊會取代**選取輸入資料表** 對話方塊。  
  
4.  按一下 [選取案例資料表] 。  
  
5.  在 **選取資料表**對話方塊中，從清單中的資料來源的 selectShifts。 在 **資料表/檢視名稱**清單中，選取 Shifts for Call Center （它可能會自動選取） 和  **確定。**  
  
     **採礦模型預測**設計介面經過更新以顯示在 輸入資料和模型中的資料行的名稱和資料類型會根據建立的對應。  
  
6.  以滑鼠右鍵按一下其中一條聯結線，然後按**修改連接**。  
  
     在此對話方塊中，您可以清楚地看到對應的資料行以及沒有對應的資料行。 採礦模型包含 Calls、Orders、IssuesRaised，以及 LvlTwoOperators 的資料行，您可以將這些資料行對應到您在來源資料中根據這些資料行所建立的任何彙總。 在這個案例中，您將對應到平均值。  
  
7.  按一下 LevelTwoOperators，旁邊的空資料格，然後選取**Shifts for Call Center.AvgOperators**。  
  
8.  按一下 Calls，選取旁邊的空資料格**Shifts for Call Center.AvgCalls**。 然後按一下**確定**。  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>若要建立每個排班的預測  
  
1.  在下方方格中的一半**預測查詢產生器**，按一下底下的空資料格**來源**，然後選取 Shifts for Call Center。  
  
2.  底下的空白資料格中**欄位**，選取 排班。  
  
3.  按一下方格中的下一個空行，然後重複上述的程序，為 [薪資類型] 加入另一個資料列。  
  
4.  在方格中，按下一個空行。 在 **來源**欄中，選取**預測函數**。 在 **欄位**欄中，選取**Predict**。  
  
5.  將 ServiceGrade 資料行從**採礦模型** 窗格下的方格中，並進入**準則/引數**資料格。 在 **別名**欄位中，輸入**預測的服務等級**。  
  
6.  在方格中，按下一個空行。 在 **來源**欄中，選取**預測函數**。 在 **欄位**欄中，選取**PredictProbability**。  
  
7.  將 ServiceGrade 資料行從**採礦模型** 窗格下的方格中，並進入**準則/引數**資料格。 在 **別名**欄位中，輸入**機率**。  
  
8.  按一下 **切換到查詢結果檢視**，檢視預測。  
  
 下表顯示每個排班的範例結果。  
  
|Shift|WageType|預測的服務等級|機率|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|假日|0.165|0.377520666|  
|midnight|假日|0.105|0.364105573|  
|PM1|假日|0.165|0.40056055|  
|PM2|假日|0.165|0.338532973|  
|AM|weekday|0.165|0.370847617|  
|midnight|weekday|0.08|0.352999173|  
|PM1|weekday|0.165|0.317419177|  
|PM2|weekday|0.105|0.311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>預測回應時間縮短對於服務等級的影響  
 您已經為每個排班產生一些平均值，並且使用這些值做為羅吉斯迴歸模型的輸入。 不過，因為商務目標是要將放棄率保持在 0.00-0.05 的範圍內，這樣結果並不令人滿意。  
  
 根據原始的模型看來，回應時間對於服務等級具有顯著的影響，因此營業小組決定執行一些預測，評估降低回應來電的平均時間是否可以提升服務品質。 例如，如果您將來電回應時間縮短為目前來電回應時間的 90% 甚至 80%，服務等級值會發生什麼情況？  
  
 建立計算每個排班之平均回應時間的資料來源檢視 (DSV)，然後新增資料行來計算該平均回應時間的 80% 或 90% 是相當容易的工作。 接著，您就可以使用 DSV 做為模型的輸入。  
  
 雖然這裡未顯示確切的步驟，但下表會比較當您將回應時間縮短為目前回應時間的 80% 或 90% 時，對服務等級造成的影響。  
  
 您可以從這些結果得出結論，也就是針對目標排班，應該將回應時間縮短為目前速率的 90%，以改進服務品質。  
  
|排班、薪資和星期幾|使用目前的平均回應時間時，預測的服務品質|回應時間縮短為 90% 時，預測的服務品質|回應時間縮短為 80% 時，預測的服務品質|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|假日 AM|0.165|0.05|0.05|  
|假日 PM1|0.05|0.05|0.05|  
|假日 Midnight|0.165|0.05|0.05|  
  
 您還可以在此模型上建立各種其他的預測查詢。 例如，您可以預測需要多少位操作員，才能達到特定的服務等級或者回應特定的來電數目。 因為在羅吉斯迴歸模型中可以加入多個輸出，所以您可以輕鬆地試驗不同的獨立變數與結果，而不需要建立許多個別的模型。  
  
## <a name="remarks"></a>備註  
 適用於 Excel 2007 的資料採礦增益集提供羅吉斯迴歸精靈，讓您輕鬆回應複雜的問題，例如，需要多少位二級操作員，才能將某個排班的服務等級提升至目標等級。 您可以免費下載資料採礦增益集，其中包含類神經網路或羅吉斯迴歸演算法的精靈。 如需詳細資訊，請參閱下列連結：  
  
-   [SQL Server 2005 資料採礦增益集適用於 Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx):搜尋目標與假設狀況分析  
  
-   [SQL Server 2008 資料採礦增益集適用於 Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790):搜尋目標狀況分析、假設狀況分析及預測計算器  
  
## <a name="conclusion"></a>結論  
 您已經學到如何建立、自訂與解譯以 Microsoft 類神經網路演算法和 Microsoft 羅吉斯迴歸演算法為基礎的採礦模型。 這些模型類型相當複雜，在分析方式上也可以有無限的變化，因此可能相當複雜且難以上手。  
  
 不過，這些演算法會逐一查看許多因數組合，並自動識別最強的互相關聯，為洞察力提供統計資料的支援，但在使用 Transact-SQL 或甚至 PowerPivot 手動瀏覽資料時難以發現此洞察力。  
  
## <a name="see-also"></a>另請參閱  
 [羅吉斯迴歸模型查詢範例](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Microsoft 羅吉斯迴歸演算法](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft Neural Network Algorithm](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [類神經網路模型查詢範例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
