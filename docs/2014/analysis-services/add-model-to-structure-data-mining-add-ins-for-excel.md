---
title: 將模型加入結構 （資料採礦適用於 Excel 的增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce68071f27897e181063299e561dfaa7d9f8aab7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062881"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>將模型加入結構 (適用於 Excel 的資料採礦增益集)
  ![將模型加入到結構按鈕](media/dmc-addmodel.gif "將模型加入結構 按鈕")  
  
 當您按一下 **將模型加入結構**，啟動精靈，可協助您建立新的採礦模型，以搭配現有的採礦結構。 這個選項可讓您比較以相同資料為基礎的模型，或是建立自訂的模型，因此會很有用。  
  
 如果 Analysis Services 執行個體尚未包含您所需的資料，使用[Create Mining Structure &#40;SQL Server 資料採礦增益集&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)精靈來設定採礦結構。 或者，您可以啟動其中一個模型精靈，然後將新模型加入由精靈所建立的結構中。  
  
 若要建立進階的模型使用精靈不支援的演算法，建立採礦結構，然後加入模型，使用**資料採礦進階查詢編輯器**。  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>將新模型加入現有的結構  
  
1.  在 **資料採礦**功能區中，按一下底下的箭號**進階**，然後選取**將模型加入結構**。  
  
2.  在 **選取結構**對話方塊方塊中，選擇包含您想要使用此項目，然後按一下 的資料結構**下一步**。  
  
     **提示**：如果您不確定哪個採礦結構包含所需的資料，使用**文件模型**檢視資料行和資料的相關基本統計資料的精靈。  
  
     如果找不到採礦結構，請檢查您目前使用的連接。 您可能需要開啟與另一部伺服器的連接。  
  
3.  在 **選取採礦演算法**對話方塊方塊中，選擇要用於新的採礦模型的採礦演算法。  
  
     請注意，對話方塊會提供比在精靈中，您會看到更多的選項。 如果您的資料相容，則可以建立使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器所支援之任何演算法的模型。  
  
4.  我們建議您也按一下**參數** 按鈕以開啟**演算法參數**對話方塊方塊中，並自訂演算法的參數。 這個選項是建立自訂採礦模型的最簡單的方式。  
  
5.  按一下 [下一步]  。  
  
6.  在 [**選取資料行**] 對話方塊中，檢閱資料行清單，並如有必要，將使用資料行變更為下列值之一：  
  
    -   **輸入**。 表示資料行所包含的變數可能會影響結果，因此應該當做模型的輸入來使用。  
  
    -   **輸入和預測**。 表示應該做為輸入的資料，您也想要預測這些值。  
  
    -   **僅預測**。 表示不應做為模型輸入的資料。  
  
    -   **索引鍵**。 每個模型至少需要一個索引鍵。 根據模型類型中，您可能也可以選擇其他的特殊索引鍵，這類 **[sequencekey]** 或是**TimeKey**。  
  
    -   **請勿使用**。 表示即使在結構中也不應在模型內使用的資料。  
  
7.  按一下瀏覽 **（...）**  按鈕以開啟**設定的資料行模型旗標** 對話方塊。  
  
     花點時間驗證每個資料行的使用方式是否適合模型。 當您嘗試處理模型時，這是防止錯誤發生的重要步驟。  
  
     例如，如果您重複使用為決策樹模型而建立的結構，並對此結構套用貝氏機率分類演算法，則需要分類收納具有資料類型 `Numeric` 和內容類型 `Continuous` 的資料行，或將其變更為離散變數。  
  
     如果在結構中的資料行不適用於新的演算法，您可以略過它們選取**請勿使用**。  
  
8.  在 [**設定的資料行模型旗標**] 對話方塊中，檢閱或設定模型旗標，如果有的話。  
  
     模型旗標可讓您控制處理 Null 的方式及執行其他作業。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](data-mining/modeling-flags-data-mining.md)。  
  
     按一下 **確定**時完成，以關閉對話方塊。  
  
9. 在 **完成**對話方塊方塊中，輸入名稱和新的採礦模型的描述。  
  
     根據您建立的模型類型而定，您可能也會擁有以下選項：  
  
    -   建立採礦模型之後，瀏覽已完成的採礦模型。  
  
    -   使用從模型到來源資料的鑽研。  
  
         如需詳細資訊，請參閱 <<c0> [ 採礦模型的鑽研](data-mining/drillthrough-on-mining-models.md)。  
  
10. 按一下 **完成**以儲存變更。 當您這樣做時，會將新模型部署到伺服器並進行處理。  
  
### <a name="related-options"></a>相關的選項  
  
|選項|註解|  
|------------|--------------|  
|**選取結構或模型**對話方塊|選擇現有的採礦結構，以做為建立新模型的基礎。  您挑選的結構必須位於目前的連接中。 如果沒有，請變更使用的連接[連接至來源的資料&#40;適用於 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)工具。|  
|**選取採礦演算法**對話方塊|此資料採礦演算法清單會視您連接的伺服器而不同。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Standard Edition 和 Enterprise Edition 提供不同的演算法。 您的管理員可能還加入了自訂演算法。<br /><br /> 如果看不到任何演算法，請確認您已連接的執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。|  
|**演算法參數**對話方塊|在這些設定中，您可以使用分析方法特定的參數來自訂每個演算法。 您也可以設定種子，以確保可跨多個定型傳遞重現模型的結果。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 演算法參數&#40;SQL Server 資料採礦增益集&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)。</c0>|  
|**設定資料行模型旗標**對話方塊|模型旗標可透過指定遺漏資料的處理方式來改善您的模型。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](data-mining/modeling-flags-data-mining.md)。|  
  
###  <a name="Bkmk_mdlcolumn"></a> 設定資料行使用方式  
 當您將新模型加入現有的採礦結構時，必須指定模型將如何在採礦結構中使用每個資料行。 此外，您可能會注意到此精靈中的選項會比採礦結構上的選項更為詳細。 為什麼？  
  
 這是因為當您使用精靈同時建立模型和結構時，會自動設定控制演算法如何使用資料的許多選項。 不過，當您將新模型加入現有的結構時，您需要手動檢視這些選項，並指定資料是否應用於分析、資料類型是否正確等等。  
  
 將新演算法套用至現有的資料時，可能會收到錯誤訊息，但這些訊息通常會提供您進行更正以處理模型所需的詳細資訊。 常見的問題包括：  
  
-   模型預期的資料類型與結構所包含的資料類型不同。  
  
     有些演算法只能處理數字，有些演算法只能處理文字。 如果您的資料類型對於新模型而言不正確，您可能需要修改結構才能處理模型。  
  
-   採礦結構沒有包含可預測的屬性。  
  
     您可以建立不含可預測值的群集模型，但其他模型通常會要求您指定單一資料行以進行預測。  
  
-   資料的撰寫是與您所選擇的演算法不相容。  
  
     某些分析類型需要資料根據獨特的規則而小心地結構化。 例如，預測模型和關聯模型。 您可以輕鬆地加入相同類型的新模型，可能包含自訂內容，但這些資料可能不適用於其他演算法。  
  
### <a name="requirements"></a>需求  
 若要建立資料採礦模型，您必須具有 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。 如需如何建立或變更連線的詳細資訊，請參閱[連接至來源的資料&#40;適用於 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 如果您看不到所需的資料採礦結構，可能是該結構儲存在不同的執行個體或不同的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中。 如需有關如何變更為不同的資料採礦連接的資訊，請參閱 <<c0> [ 連接到資料採礦伺服器](connect-to-a-data-mining-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
