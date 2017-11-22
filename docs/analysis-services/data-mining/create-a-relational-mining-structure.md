---
title: "建立關聯式採礦結構 |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- data mining [Analysis Services], structure
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
- OLAP mining models [Analysis Services]
ms.assetid: 5547d639-377d-4ca7-88fc-ce1f9e2babc5
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3d58cb5bf4be5eddaa40cc13efa88b3ade9f49dd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-relational-mining-structure"></a>建立關聯式採礦結構
  大多數的資料採礦模型都是根據關聯式資料來源。 建立關聯式資料採礦模型的優點如下：您可以組合隨選資料及定型和更新模型，而不需要經歷建立 Cube 的複雜程序。  
  
 關聯式採礦結構可以繪製不同來源的資料。 原始資料可以儲存在資料表、檔案或關聯式資料庫系統中，前提是這些資料可以定義為資料來源檢視的一部分。 例如，如果您的資料在 Excel 中、SQL Server 資料倉儲中或 SQL Server 報表資料庫中，或是在透過 OLE DB 或 ODBC 提供者所存取的外部來源中，您應該使用關聯式採礦結構。  
  
 本主題提供如何使用資料採礦精靈建立關聯式採礦結構的概觀。  
  
 [需求](#BKMK_Relational_Structure)  
  
 [建立關聯式採礦結構的程序](#BKMK_Relational_Structure)  
  
 [如何選擇資料來源](#BKMK_ChooseRelData)  
  
 [如何指定內容類型和資料類型](#bkmk_ContentDataType)  
  
 [如何及為何建立鑑效組資料集](#bkmk_Holdout)  
  
 [如何及為何啟用鑽研](#BKMK_DrillThru)  
  
## <a name="requirements"></a>需求  
 首先，您必須擁有現有的資料來源。 您可以使用資料來源設計師來設定資料來源 (如果沒有資料來源存在的話)。 如需詳細資訊，請參閱[建立資料來源 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)。  
  
 接下來，請使用資料來源檢視精靈，將必要的資料組合成單一資料來源檢視。 如需如何使用資料來源檢視選取、轉換、篩選或管理資料的詳細資訊，請參閱 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
##  <a name="BKMK_Relational_Structure"></a> 程序概觀  
 在方案總管中，以滑鼠右鍵按一下 [採礦結構] 節點，然後選取 [新增採礦結構]，即可啟動資料採礦精靈。 此精靈會引導您透過下列步驟來建立新關聯式採礦模型的結構：  
  
1.  **選取定義方法**：您可以在這裡選取資料來源類型，並選擇 [從現有的關聯式資料庫或資料倉儲]。  
  
2.  **建立資料採礦結構**：決定只要建立結構，還是建立包含採礦模型的結構。  
  
     您也會選擇適合初始模型的演算法。 如需哪一個演算法最適合某些工作的指示，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
3.  **選取資料來源檢視**：選擇用於定型模型的資料來源檢視。 此資料來源檢視也可以包含用於測試的資料或是不相關的資料。 您必須挑選哪些資料會實際用於此結構和模型中。 您之後也可以為資料套用篩選。  
  
4.  **指定資料表類型**：選取包含用於分析之案例的資料表。 對於某些資料集而言，特別是用來建立購物籃模型的資料集，您可能也會包含相關資料表來當做巢狀資料表使用。  
  
     對於每一個資料表，您都必須指定索引鍵，如此一來，當您已加入巢狀資料表時，演算法就會知道如何識別唯一記錄和相關記錄。  
  
     如需詳細資訊，請參閱 [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md)。  
  
5.  **指定定型資料**：在這個頁面上，您會選擇「案例資料表」，這是包含最重要之分析資料的資料表。  
  
     對於某些資料集而言，特別是用來建立購物籃模型的資料集，您可能也會包含相關資料表。 該巢狀資料表中的值將會當做多個值來處理，這些值全都與主資料表中的單一資料列 (或案例) 有關。  
  
6.  **指定資料行的內容和資料類型**：對於您在結構中使用的每一個資料行，您都必須選擇「資料類型」和「內容類型」。  
  
     此精靈將會自動偵測可能的資料類型，但是您不需要使用此精靈所建議的資料類型。 例如，即使您的資料包含數字，還是可能會代表類別資料。 系統會針對該特定模型類型，為您指定為索引鍵的資料行自動指派正確的資料類型。 如需詳細資訊，請參閱[採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)和[資料類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/data-types-data-mining.md)。  
  
     您針對模型中所使用之每一個資料行所選擇的 *「內容類型」* 會告訴演算法應該如何處理資料。  
  
     例如，您可能會決定離散化數字，而不是使用連續的值。 您也可以要求演算法自動為資料行偵測最好的內容類型。 如需詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
7.  **建立測試集**：您可以在這個頁面上告訴精靈，應該將多少資料數量保留給測試模型使用。 如果您的資料將支援多個模型，則建立鑑效組資料集是一個很好的作法，這樣可以針對相同的資料測試所有模型。  
  
     如需詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
8.  **正在完成精靈**：在這個頁面上，您可以為新的採礦結構和關聯的採礦模型提供名稱，並儲存此結構和模型。  
  
     您也可以根據模型類型來設定一些重要的選項。 例如，您可以在結構上啟用鑽研。  
  
     此時，採礦結構和其模型都只是中繼資料，您需要加以處理才能得到結果。  
  
##  <a name="BKMK_ChooseRelData"></a> 如何選擇關聯式資料  
 關聯式採礦結構能夠以透過 OLE DB 資料來源取得的任何資料為基礎。 如果來源資料包含在多份資料表內，您會使用資料來源檢視，將您需要的資料表與資料行組合在一個地方。  
  
 如果資料表包含任何一對多關聯性 (例如，對於每一個想要分析的客戶都有多筆訂購記錄)，那麼您可以同時加入兩個資料表，然後使用其中一個資料表做為案例資料表，將關聯性多側中的資料連結為巢狀資料表。  
  
 採礦結構中的資料是衍生自現有資料來源檢視中的任何內容。 您可以視需要修改資料來源檢視中的資料，加入在基礎關聯式資料中可能不存在的關聯性或衍生的資料行。 您也可以在資料來源檢視內建立具名的計算或彙總。 如果您對於資料來源中的資料排列方式沒有控制權，或者如果您想要試驗資料採礦模型的不同資料彙總，這些功能會非常實用。  
  
 您不必使用所有提供的資料，您可以挑選並選擇要將哪些資料行包含在採礦結構中。 然後以該結構為基礎的所有模型都可以使用這些資料行，或者您可以針對特定模型將某些資料行標示為 **Ignore** 。 您甚至可以讓資料採礦模型的使用者從採礦模型的結果進行鑽研，以查看未包含在採礦模型本身中的其他採礦結構資料行。  
  
##  <a name="bkmk_ContentDataType"></a> 如何指定內容類型和資料類型  
 此資料類型與您在 SQL Server 或其他應用程式介面中指定的資料類型大致相同：日期和時間、不同大小的數目、布林值、文字和其他離散資料。  
  
 但是，內容類型對於資料採礦非常重要而且會影響分析的結果。 內容類型會告訴演算法應該對資料採取何種處理方式：應該處理連續小數位數的數字還是進行分類收納？ 有多少可能的值？ 每一個值是否相異？ 如果值為索引鍵，它是什麼種類的索引鍵 -- 它表示日期/時間值、序列還是某種其他類型的索引鍵？  
  
 請注意，您選擇的資料類型可以限制您選擇的內容類型。 例如，您不能將非數值的值離散化。 如果您看不到您想要的內容類型，您可以按一下 [上一步] 返回資料類型頁面，並嘗試不同的資料類型。  
  
 您不需要過於擔心得到錯誤的內容類型。 建立新的模型以及變更模型中的內容類型非常簡單，前提是採礦結構中的資料類型集合可支援新的內容類型。 使用不同的內容類型建立多個模型 (當做試驗或是符合不同演算法的需求) 也很常見。  
  
 例如，如果您的資料包含收入資料行，則當您使用 Microsoft 決策樹演算法時可能會建立兩個不同的模型，並另外將資料行設定為連續數字或離散的範圍。 但是，如果您已使用 Microsoft 貝氏機率分類演算法加入模型，您會被強制將此資料行變更為僅限離散化的值，因為該演算法不支援連續數字。  
  
##  <a name="bkmk_Holdout"></a> 為何及如何將資料分割成定型集和測試集  
 在接近精靈結尾處，您必須決定是否要將資料分割成定型集和測試集。 佈建隨機取樣的資料部分以供測試的功能非常方便，因為這樣可確保所有與新採礦結構相關聯的採礦模型都能使用一致的測試資料集。  
  
> [!WARNING]  
>  請注意，並非所有模型類型都可使用此選項。 例如，如果您建立預測模型，您將無法使用鑑效組，因為時間序列演算法要求資料中不得有間距。 如需支援鑑效組資料集之模型類型的清單，請參閱 [定型和測試資料集](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
 若要建立這個鑑效組資料集，您會指定想要用於測試之資料的百分比。 所有其餘資料將會用於定型。 您也可以選擇設定要用於測試的案例數目上限，或者設定啟動隨機選擇程序所要使用的初始值。  
  
 鑑效組測試集的定義會與採礦結構儲存在一起，所以每當您根據結構建立新模型時，就可以使用測試資料集來評估模型的精確度。 如果您刪除採礦結構的快取，則有關哪些案例用於定型及哪些案例用於測試的資訊也會一併刪除。  
  
##  <a name="BKMK_DrillThru"></a> 如何及為何啟用鑽研  
 在精靈的結尾處，您可以選擇啟用「鑽研」。 這個選項很容易被遺漏，但是卻非常重要。 鑽研可讓您透過查詢採礦模型，檢視採礦結構中的來源資料。  
  
 為什麼很實用？ 假設您正在檢視群集模型的結果，而且想要查看被置於特定叢集的客戶。 您可以使用鑽研來檢視類似連絡資訊的詳細資料。  
  
> [!WARNING]  
>  若要使用鑽研，當您建立採礦結構時必須啟用鑽研。 您之後可以在模型上設定屬性，於模型上啟用鑽研，但是採礦結構要求一開始就應該設定這個選項。 如需詳細資訊，請參閱[鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦設計師](../../analysis-services/data-mining/data-mining-designer.md)   
 [資料採礦精靈 &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)   
 [採礦模型屬性](../../analysis-services/data-mining/mining-model-properties.md)   
 [採礦結構和結構資料行的屬性](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)   
 [採礦結構工作和操作說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
