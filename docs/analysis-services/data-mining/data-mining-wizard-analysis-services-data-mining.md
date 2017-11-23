---
title: "資料採礦精靈 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
caps.latest.revision: "57"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ad9dd40bb7f7f8da0820d9ccbefafed9079650b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>資料採礦精靈 (Analysis Services - 資料採礦)
  每次將新的採礦結構加入至資料採礦專案時， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的資料採礦精靈就會啟動。 此精靈可幫助您選擇資料來源及設定資料來源檢視來定義用於分析的資料，然後幫助您建立初始模型。  
  
 在精靈的最後一個階段，您可以選擇將資料分成定型集和測試集，並啟用類似鑽研的功能。  
  
## <a name="what-to-know-before-you-start"></a>開始之前應該知道的事項  
 以下是啟動精靈之前所需要知道的事項。  
  
-   是否要從關聯式資料庫或從 OLAP 資料庫之現有的 Cube 中，建立資料採礦結構和模型？  
  
-   哪些資料行包含了可唯一識別案例記錄的索引鍵？  
  
-   您想要使用哪些資料行或屬性來預測？ 哪些資料行或屬性非常適合當做分析的輸入使用？  
  
-   您應該使用哪一個演算法？ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的演算法各具有不同的特性，且會產生不同的結果。 很幸運的是，每一組資料不限於一個模型，所以您可以自由地加入不同的模型進行試驗。  
  
-   您是否需要能夠針對統一的資料集測試模型？ 如果是的話，請考慮使用此選項，以保留某些資料進行測試。 您可以選擇某個百分比，然後視需要加以覆蓋指定的資料列數。  
  
##  <a name="BKMK_Using_DM_Wizard"></a> 啟動資料採礦精靈  
 若要使用資料採礦精靈，您必須已在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開啟方案，此方案至少包含一個資料採礦或 OLAP 專案。  
  
-   如果您的方案已經準備好進行資料採礦，您只需要以滑鼠右鍵按一下方案總管中的 [採礦結構] 節點，然後選取 [新增採礦結構]，即可啟動此精靈。  
  
-   如果您的方案不包含任何現有專案，您可以加入新的資料採礦專案。 從 [檔案] 功能表選取 [新增]，再選取 [專案]。 請務必選擇 [Analysis Services 多維度和資料採礦專案] 範本。  
  
-   您也可以使用 Analysis Services 匯入精靈，從現有的資料採礦方案取得中繼資料。 但是，您不能選取個別物件來匯入，整個資料庫都要匯入，包括任何 Cube、資料來源檢視等。也請注意，透過匯入建立的新方案會自動設定為使用本機預設資料庫。 您可能需要將此設定變更為另一個執行個體，然後才可以處理或瀏覽物件，而且如果您從舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 匯入，您可能需要更新提供者的參考。  
  
 接下來，您將會建立採礦結構以及一個相關聯的資料採礦模型。 您也可以只建立採礦結構，並在之後加入模型，但是先建立測試模型通常是最容易的方式。  
  
###  <a name="BKMK_Relational"></a>關聯式與OLAP 採礦模型的比較  
 下一個重要的選項是選擇是否使用關聯式資料來源，或是讓您的模型根據多維度 (OLAP) 資料。  
  
 資料採礦精靈會在這個點分成兩個路徑，這取決於您的資料來源為關聯式或是在 Cube 中。 資料選取程序以外的所有內容都相同，包括演算法的選擇、加入鑑效組資料集的能力等，但是選取 Cube 資料要比使用關聯式資料複雜一些 (如果您建立的模型是以 Cube 為根據，最後您也可以取得一些其他選項)。  
  
 如需每一個選項的詳細逐步解說，請參閱以下主題：  
  
 [建立關聯式採礦結構](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 在您建立關聯式資料採礦模型時，引導您進行決策。  
  
 [建立 OLAP 採礦結構](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 描述當您從 OLAP Cube 中選擇資料時所做的其他選項和選擇。  
  
> [!NOTE]  
>  您不需要 Cube 或 OLAP 資料庫，也可以進行資料採礦。 除非您的資料已儲存在 Cube 中，或是您想要採礦 OLAP 維度或是 OLAP 彙總或計算的結果，否則我們建議您針對資料採礦使用關聯式資料表或資料來源。  
  
### <a name="choosing-an-algorithm"></a>選擇演算法  
 接下來，您必須決定要使用哪一個演算法來處理資料。 這個決定可能很困難。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的每一個演算法都有不同的功能而且會產生不同的結果，所以您可以試驗並嘗試幾個不同模型，然後再決定哪一個模型最適合您的資料和商業問題。 如需每一個演算法最適合之工作的說明，請參閱以下主題：  
  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 同樣地，您可以使用不同的演算法建立多個模型，或變更演算法的參數以建立不同的模型。 系統不會限制您的演算法選擇，針對相同資料建立幾個不同模型也是很好的作法。  
  
### <a name="define-the-data-used-for-modeling"></a>定義用於模型化的資料  
 除了從來源中選擇資料以外，您也必須指定資料來源檢視中的哪一個資料表包含「案例資料」。 案例資料表將會用來定型資料採礦模型，因此您應該包含您想要分析的實體：例如，客戶和客戶的人口統計資訊。 每一個案例都必須是獨一無二的，而且必須可由「案例索引鍵」 識別。  
  
 除了指定案例資料表以外，您也可以在資料中包含「巢狀資料表」。 巢狀資料表通常會包含有關案例資料表內實體 (例如客戶所進行之交易) 的詳細資訊，或是與實體具有多對一關聯性的屬性。 例如，聯結到 **Customers** 案例資料表的巢狀資料表可能包含每個客戶所購買的產品清單。 在分析網站流量的模型中，巢狀資料表可能會包含使用者造訪之頁面的順序。 如需詳細資訊，請參閱[巢狀資料表 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
### <a name="additional-features"></a>其他功能  
 為了協助您選擇正確的資料，並正確設定資料來源，資料採礦精靈會提供以下其他功能：  
  
-   **自動偵測資料類型**：此精靈將會檢查資料行值的唯一性與分佈，然後建議最佳資料類型和資料的使用類型。 您可以從清單中選取值來覆寫這些建議。  
  
-   **變數的建議**：您可以在對話方塊上按一下，並啟動分析器來計算模型包含的資料行之間的相互關聯性，並判斷是否有任何資料行可能是結果屬性的預測指標 (在給定目前的模型組態之下)。 您可以輸入不同的值來覆寫這些建議。  
  
-   **特徵選取**：大多數的演算法都會自動偵測屬於良好預測指標的資料行，並優先使用這些資料行。 如果資料行中包含太多的值，則會套用「特徵選取」，以減少資料的基數，並提升找到有意義模式的機率。 您可以使用模型參數來影響特徵選取行為。  
  
-   **自動配量 Cube**：如果採礦模型是以 OLAP 資料來源為基礎，則會自動提供使用 Cube 屬性配量模型的功能。 這對於根據 Cube 資料的子集來建立模型非常實用。  
  
### <a name="completing-the-wizard"></a>正在完成精靈  
 此精靈中的最後一個步驟為命名採礦結構和相關聯的採礦模型。 根據您建立的模型類型而定，您可能也會擁有以下的重要選項：  
  
-   如果您選取 [允許使用鑽研]，就會在模型中啟用「鑽研」(drill through) 功能。 有了鑽研功能，具有適當權限的使用者便可以瀏覽用來建立此模型的來源資料。  
  
-   如果您正在建立 OLAP 模型，您可以選取 [Create a data mining dimension (建立新的資料採礦 Cube)] 或 [建立資料採礦維度] 選項。 這兩個選項都可讓您輕鬆瀏覽完成的模型，並鑽研至基礎資料。  
  
 完成資料採礦精靈之後，您可以使用資料採礦設計師來修改採礦結構和模型、檢視模型的精確度、檢視結構和模型的特性，或使用模型進行預測。  
  
 [回到頁首](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>相關內容  
 若要深入了解當您建立資料採礦模型時所需要做的決策，請參閱以下連結：  
  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 [內容類型 (資料採礦)](../../analysis-services/data-mining/content-types-data-mining.md)  
  
 [資料類型 (資料採礦)](../../analysis-services/data-mining/data-types-data-mining.md)  
  
 [特徵選取 &#40;資料採礦&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md)  
  
 [遺漏值 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)  
  
 [採礦模型的鑽研](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦工具。](../../analysis-services/data-mining/data-mining-tools.md)   
 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
