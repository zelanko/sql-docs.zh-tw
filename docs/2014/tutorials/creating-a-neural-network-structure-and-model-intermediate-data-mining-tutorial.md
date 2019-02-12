---
title: 建立類神經網路結構和模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56037719"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>建立類神經網路結構和模型 (中繼資料採礦教學課程)
  若要建立資料採礦模型，您必須先使用「資料採礦精靈」，根據新的資料來源檢視建立新的採礦結構。 在這項工作中，您將利用這個精靈來建立採礦結構，並同時根據 [!INCLUDE[msCoName](../includes/msconame-md.md)] 類神經網路演算法來建立關聯的採礦模型。  
  
 類神經網路相當靈活，可以分析許多輸入和輸出的組合，因此，您應該試驗數種處理資料的方式，以取得最佳的結果。 例如，您可能想要自訂服務品質的數值目標的方式*分類收納*，或群組，指向特定的業務需求。 若要這樣做，您將會以不同的方式將新的資料行加入到可分組數值資料的採礦結構中，然後建立一個模型來使用這個新的資料行。 您將會使用這些採礦模型來執行一些探索。  
  
 最後，當您得知類神經網路模型中哪些因素對於您的商務問題有最大的影響力時，您將會建立個別的模型來進行預測及計分。 您將會使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 羅吉斯迴歸演算法，此演算法是根據類神經網路模型，但是已經最佳化，可根據特定輸入來尋找方案。  
  
 **步驟**  
  
 [建立預設採礦結構和模型](#bkmk_defaul)  
  
 [使用離散化來儲藏可預測資料行](#bkmk_ColumnCopy)  
  
 [複製資料行並變更不同模型的離散化方法](#bkmk_Alias)  
  
 [建立可預測資料行的別名，因此，您可以比較模型](#bkmk_Alias2)  
  
 [處理所有模型](#bkmk_SeedProcess)  
  
## 建立預設客服中心結構  <a name="bkmk_defaul"></a>  
  
1.  在 [方案總管] 中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下**採礦結構**，然後選取**New Mining Structure&lt**。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在 [**選取定義方法**頁面上，確認**從現有的關聯式資料庫或資料倉儲**已選取，然後按一下**下一步]**。  
  
4.  在 **建立資料採礦結構**頁面上，確認選項**建立採礦結構與採礦模型**已選取。  
  
5.  按一下下拉式清單選項**您想要使用哪一種資料採礦技術？**，然後選取**Microsoft 類神經網路**。  
  
     羅吉斯迴歸模型是以類神經網路為基礎，因此，您可以重複使用相同的結構，並加入新的採礦模型。  
  
6.  按一下 [下一步] 。  
  
     **選取資料來源檢視**頁面隨即出現。  
  
7.  底下**可用的資料來源檢視**，選取`Call Center`，然後按一下**下一步**。  
  
8.  在 **指定資料表類型**頁面上，選取**案例**旁的核取方塊**FactCallCenter**資料表。 未選取任何項目如**DimDate**。 按一下 [下一步] 。  
  
9. 在 **指定培訓資料**頁面上，選取**金鑰**資料行旁邊**FactCallCenterID。**  
  
10. 選取 `Predict`並**輸入**核取方塊。  
  
11. 選取 **金鑰**，**輸入**，和`Predict`核取方塊下, 表所示：  
  
    |資料表/資料行|索引鍵/輸入/預測|  
    |---------------------|-------------------------|  
    |AutomaticResponses|輸入|  
    |AverageTimePerIssue|輸入/預測|  
    |Calls|輸入|  
    |DateKey|請勿使用|  
    |DayOfWeek|輸入|  
    |FactCallCenterID|Key|  
    |IssuesRaised|輸入|  
    |LevelOneOperators|輸入/預測|  
    |LevelTwoOperators|輸入|  
    |Orders|輸入/預測|  
    |ServiceGrade|輸入/預測|  
    |Shift|輸入|  
    |TotalOperators|請勿使用|  
    |WageType|輸入|  
  
     請注意，多個可預測資料行已選取。 類神經網路演算法的強項之一是，它可以分析所有可能的輸入和輸出屬性組合。 因為它無法以指數方式增加處理時間，您不想要對大型資料集，執行此動作...  
  
12. 在 [**指定資料行的內容和資料類型**頁面上，確認此方格有包含資料行、 內容類型和下表所示的資料類型，然後按一下**下一步]**。  
  
    |[資料行]|內容類型|資料型別|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|Continuous|長整數|  
    |AverageTimePerIssue|Continuous|長整數|  
    |Calls|Continuous|長整數|  
    |DayOfWeek|Discrete|文字|  
    |FactCallCenterID|Key|長整數|  
    |IssuesRaised|Continuous|長整數|  
    |LevelOneOperators|Continuous|長整數|  
    |LevelTwoOperators|Continuous|長整數|  
    |Orders|Continuous|長整數|  
    |ServiceGrade|Continuous|Double|  
    |Shift|Discrete|文字|  
    |WageType|Discrete|文字|  
  
13. 在 **建立測試設定**頁面上，清除該選項的文字方塊**測試資料的百分比**。 按一下 [下一步] 。  
  
14. 在上**完成精靈**頁面上，如**採礦結構名稱**，型別`Call Center`。  
  
15. 針對**採礦模型名稱**，型別`Call Center Default NN`，然後按一下**完成**。  
  
     **允許使用鑽研**方塊已停用，因為您無法鑽研與類神經網路模型的資料。  
  
16. 在 [方案總管] 中，以滑鼠右鍵按一下您剛才資料採礦結構的名稱建立，然後選取**程序**。  
  
## <a name="use-discretization-to-bin-the-target-column"></a>使用離散化來儲藏目標資料行  
 根據預設，當您建立具有數值之可預測屬性的類神經網路模型時，Microsoft 類神經網路演算法會將該屬性視為一個連續數字。 例如，ServiceGrade 屬性是一個理論上範圍從 0.00 (已接聽所有電話) 到 1.00 (已掛斷所有呼叫端) 的數字。 在此資料集中，值的分佈如下：  
  
 ![服務等級值的分佈](../../2014/tutorials/media/skt-service-grade-valuesc.gif "發佈的服務等級值")  
  
 因此，當您處理模型時，輸出結果的群組方式可能會和您預期的不同。 比方說，如果您使用叢集來識別值的最佳群組，演算法會將 ServiceGrade 值分成多個這類的範圍：0.0748051948 - 0.09716216215. 雖然這個群組在數學上是正確的，但是這些範圍對商務使用者而言，可能沒有很大的意義。  
  
 在此步驟中，若要讓結果更直覺化，您會將數值分組以不同的方式，建立數值資料行的複本。  
  
### <a name="how-discretization-works"></a>離散化的運作方式  
 Analysis Services 會提供各種方法來分類收納或處理數值資料。 下表說明當輸出屬性 ServiceGrade 已處理三種不同的方式之後，所產生的結果之間的差異：  
  
-   將其視為連續的數字。  
  
-   讓演算法使用叢集來識別值的最佳排列。  
  
-   指定數字要透過 Equal Areas 方法進行分類收納。  
  
 預設模型 (連續)  
  
|Value|SUPPORT|  
|-----------|-------------|  
|Missing|0|  
|0.09875|120|  
  
 透過叢集進行分類收納  
  
|Value|SUPPORT|  
|-----------|-------------|  
|\< 0.0748051948|34|  
|0.0748051948 - 0.09716216215|27|  
|0.09716216215 - 0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 透過同等區域進行分類收納  
  
|Value|SUPPORT|  
|-----------|-------------|  
|\< 0.07|26|  
|0.07 - 0.00|22|  
|0.09 - 0.11|36|  
|>= 0.12|36|  
  
> [!NOTE]  
>  當所有資料都經過處理之後，您就可以從模型的臨界統計資料節點取得這些統計資料。 如需有關臨界統計資料節點的詳細資訊，請參閱[Mining Model Content for Neural Network Models &#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)。  
  
 在此表中，VALUE 資料行顯示如何處理 ServiceGrade 的數字。 SUPPORT 資料行顯示多少案例有該值，或在該範圍中。  
  
-   **使用連續數字 （預設值）**  
  
     如果您使用預設方法，演算法會計算 120 個相異值的結果，其平均值為 0.09875。 您也可以看到遺漏值的數目。  
  
-   **透過叢集進行分類收納**  
  
     當您讓 Microsoft 叢集演算法決定值的選擇性群組方式時，演算法會將 ServiceGrade 的值群組為五 (5) 個範圍。 從 SUPPORT 資料行可得知，案例數目未平均分佈在各範圍中。  
  
-   **透過同等區域進行分類收納**  
  
     當您選擇此方法時，演算法會強制將值分為相同大小的貯體，這又會變更各範圍的上下限。 您可以指定貯體的數目，但要避免貯體中有太少的值。  
  
 如需有關分類收納選項的詳細資訊，請參閱 <<c0> [ 離散化方法&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md)。</c0>  
  
 或者，而不是使用數字的值，您可以新增個別的衍生資料行，將服務等級分類成預先定義的目標範圍，例如**最佳**(ServiceGrade \<= 0.05)、 **可接受**(0.10 > ServiceGrade > 0.05)，並**不良**(ServiceGrade > = 0.10)。  
  
###  <a name="bkmk_newColumn"></a> 建立資料行的複本，並變更離散化方法  
 您將建立一份包含目標屬性 ServiceGrade 的採礦資料行，並變更數字分組的方式。 您可以在採礦結構中建立任何資料行的多個複本，包括可預測的屬性。  
  
 在此教學課程中，您將會使用離散化的 Equal Areas 方法，並指定四個貯體。 這個方法所產生的群組與商務使用者感興趣的目標值非常接近。  
  
####  <a name="bkmk_ColumnCopy"></a> 若要建立採礦結構中的資料行的自訂的複本  
  
1.  在 [方案總管] 中，按兩下您剛剛建立的採礦結構。  
  
2.  在 [採礦結構] 索引標籤中，按一下**加入採礦結構資料行**。  
  
3.  在 **選取資料行** 對話方塊中，從清單中選取 ServiceGrade**來源資料行**，然後按一下 **確定**。  
  
     新的資料行就會加入到採礦結構資料行的清單中。 根據預設，新的採礦資料行與現有資料行同名，但是後面多加了一個數值，例如 ServiceGrade 1。 您可以變更此資料行的名稱，使名稱更具描述性。  
  
     您也將指定離散化方法。  
  
4.  以滑鼠右鍵按一下 ServiceGrade 1，然後選取**屬性**。  
  
5.  在 [**屬性**] 視窗中，找出**名稱**屬性，並將名稱變更為**Service Grade Binned** 。  
  
6.  隨即出現一個對話方塊，詢問您是否要針對所有相關採礦模型資料行的名稱進行相同的變更。 按一下 **[否]**。  
  
7.  在 [**屬性**] 視窗中，找出區段**資料型別**並視需要展開它。  
  
8.  將屬性 `Content` 的值從 `Continuous` 變更為 `Discretized`。  
  
     現在有下列屬性可以使用。 變更屬性值，如下表所示：  
  
    |屬性|預設值|新值|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|沒有值|4|  
  
    > [!NOTE]  
    >  <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 的預設值實際上是 0，這表示演算法會自動決定最佳的貯體數目。 因此，如果您想要將此屬性的值重設為其預設值，請輸入 0。  
  
9. 在 [資料採礦設計師中，按一下**採礦模型**] 索引標籤。  
  
     請注意，當您加入採礦結構資料行的複本時，此複本的使用旗標會自動設定為 `Ignore`。 通常當您在採礦結構中加入資料行的複本時，您不會搭配原始資料行來使用此複本進行分析，否則演算法將會在兩個資料行之間尋找很強的關聯，這樣可能會遮蔽其他關聯性。  
  
##  <a name="bkmk_NewModel"></a> 將新的採礦模型加入採礦結構  
 現在您已經針對目標屬性建立新的群組，所以需要加入一個新的採礦模型來使用離散化資料行。 當您完成時，CallCenter 採礦結構將會有兩個採礦模型：  
  
-   「撥接中心預設 NN」採礦模型會將 ServiceGrade 值當做連續範圍來處理。  
  
-   您將建立新的採礦模型，撥接中心 Binned NN，可做為其目標結果的 [ServiceGrade] 資料行，分佈在四個貯體大小相同的值。  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>若要根據新的離散化資料行來加入採礦模型  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下您剛才的採礦結構建立，然後選取**開啟**。  
  
2.  按一下 **[採礦模型]** 索引標籤。  
  
3.  按一下 **建立相關的採礦模型**。  
  
4.  在**新的採礦模型** 對話方塊中，如**模型名稱**，型別`Call Center Binned NN`。 在 **演算法名稱**下拉式清單中選取**Microsoft 類神經網路**。  
  
5.  在新的採礦模型所包含的資料行清單中，尋找 ServiceGrade，然後將使用方式從 `Predict` 變更為 `Ignore`。  
  
6.  同樣地，找出 ServiceGrade Binned，然後將使用方式從 `Ignore` 變更為 `Predict`。  
  
##  <a name="bkmk_Alias2"></a> 建立目標資料行的別名  
 一般來說，您無法比較使用不同可預測屬性的採礦模型。 但是您可以為採礦模型資料行建立別名。 也就是您可以重新命名資料行，ServiceGrade Binned，採礦模型中的，使其具有與原始資料行同名。 然後您可以在精確度圖表中直接比較這兩個模型，即使資料是以不同方式離散化也可以。  
  
###  <a name="bkmk_Alias"></a> 若要在採礦模型加入採礦結構資料行的別名  
  
1.  在  **Mining Models**索引標籤之下**結構**，選取 ServiceGrade Binned。  
  
     請注意，**屬性**視窗會顯示物件，也就是 scalarminingstructure 資料行的屬性。  
  
2.  在採礦模型的 [ServiceGrade Binned NN] 資料行底下，按一下與 [ServiceGrade Binned] 資料行對應的資料格。  
  
     請注意，現在**屬性**視窗會顯示 MiningModelColumn 物件的屬性。  
  
3.  找出**名稱**屬性，並將值變更為`ServiceGrade`。  
  
4.  找出**描述**屬性，並輸入**暫時資料行別名**。  
  
     **屬性**視窗應該包含下列資訊：  
  
    |屬性|值|  
    |--------------|-----------|  
    |**說明**|暫時資料行別名|  
    |**ID**|ServiceGrade Binned|  
    |**模型旗標**||  
    |**名稱**|服務等級|  
    |**SourceColumn ID**|服務等級 1|  
    |**Usage**|Predict|  
  
5.  按一下任何地方**採礦模型** 索引標籤。  
  
     此方格會更新以顯示新的暫時資料行別名， `ServiceGrade`，資料行使用方式旁。 包含採礦結構及兩個採礦模型的方格應該如下所示：  
  
    |結構|撥接中心預設 NN|分類收納的撥接中心 NN|  
    |---------------|----------------------------|---------------------------|  
    ||Microsoft 類神經網路|Microsoft 類神經網路|  
    |AutomaticResponses|輸入|輸入|  
    |AverageTimePerIssue|Predict|Predict|  
    |Calls|輸入|輸入|  
    |DayOfWeek|輸入|輸入|  
    |FactCallCenterID|Key|Key|  
    |IssuesRaised|輸入|輸入|  
    |LevelOneOperators|輸入|輸入|  
    |LevelTwoOperators|輸入|輸入|  
    |Orders|輸入|輸入|  
    |ServceGrade Binned|Ignore|Predict (ServiceGrade)|  
    |ServiceGrade|Predict|Ignore|  
    |Shift|輸入|輸入|  
    |Total Operators|輸入|輸入|  
    |WageType|輸入|輸入|  
  
## <a name="process-all-models"></a>處理所有模型  
 最後，為了確認您建立的模型可以輕鬆比較，您將會針對預設模型和分類收納模型設定種子參數。 設定初始值可保證每一個模型都會從相同點開始處理資料。  
  
> [!NOTE]  
>  如果您沒有為種子參數指定一個數值，SQL Server Analysis Services 將會根據模型的名稱產生一個種子。 因為模型的名稱永遠不同，因此您必須設定一個初始值，以確保它們會以相同順序處理資料。  
  
###  <a name="bkmk_SeedProcess"></a> 若要指定種子和處理模型  
  
1.  在 **採礦模型**索引標籤，以滑鼠右鍵按一下資料行的模型名稱為撥接中心-LR，然後選取**設定演算法參數**。  
  
2.  在 HOLDOUT_SEED 參數的資料列，按一下 底下的空資料格**值**，然後輸入`1`。 按一下 [確定] 。 針對與此結構有關的每一個模型重複這個步驟。  
  
    > [!NOTE]  
    >  只要您將相同的種子用於所有相關的模型，您選擇做為種子的值就不重要了。  
  
3.  在  **Mining Models**功能表上，選取**處理採礦結構和所有模型**。 按一下 **是**若要更新的資料採礦專案部署至伺服器。  
  
4.  在 [**處理採礦模型**] 對話方塊中，按一下**執行**。  
  
5.  按一下 [**關閉**以關閉**處理進度**對話方塊，然後再按一下**關閉**中再次**處理採礦模型**] 對話方塊。  
  
 現在您已經建立兩個相關的採礦模型，您將會瀏覽資料來探索資料的關聯性。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [探索撥接中心模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構 &#40;Analysis Services-資料採礦 &#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
