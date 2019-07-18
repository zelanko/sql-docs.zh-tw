---
title: 處理目標的郵寄結構 （基本資料採礦教學課程） 中的模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188233"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>處理目標郵寄結構中的模型 (基本資料採礦教學課程)
  在您可以瀏覽或使用採礦模型之前，必須先部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案並處理採礦結構和採礦模型。  
  
-   *部署*傳送到伺服器的專案，並在伺服器上該專案中建立任何物件。  
  
-   *處理*填入[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]與關聯式資料來源的資料物件。  
  
 模型要等到部署及處理之後，才可以使用。 此外，一旦您對模型進行任何變更 (例如加入新資料)，就必須重新部署及重新處理模型。  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>確保與 HoldoutSeed 之間的一致性  
 當您部署專案以及處理結構與模型時，資料結構中的個別資料列將會指派給以數值種子值為根據的定型集或測試集。 依預設，數值種子值是根據資料結構中的屬性來計算。 不過，如果您變更了模型的某些層面，種子值將會變更而使得結果稍微不同。 因此，為了確保您的結果會如同以下所述，我們將會任意指派固定*鑑效組種子*的`12`。 鑑效組種子是用來初始化取樣演算法，並確保所有採礦結構及其模型的資料分割方式大致相同。  
  
 這個值不會影響定型集內的案例數目，而是要確保每次建立模型時都將使用相同的資料分割方法。  
  
 如需有關鑑效組種子的詳細資訊，請參閱 <<c0> [ 定型和測試資料集](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
#### <a name="to-set-the-holdout-seed"></a>若要設定鑑效組種子  
  
1.  按一下**Mining Structure**  索引標籤或**採礦模型** 索引標籤中的資料採礦設計師中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
     **目標郵寄 MiningStructure**中會顯示**屬性**窗格。  
  
2.  請確認**屬性**藉由按下窗格會開啟**F4**。  
  
3.  請確認**CacheMode**設為**KeepTrainingCases**。  
  
4.  請輸入`12`for **HoldoutSeed**。  
  
## <a name="deploying-and-processing-the-models"></a>部署及處理模型  
 在資料採礦設計師中，您可以決定哪一個要處理物件，視您已對您的模型或基礎資料變更的範圍而定：  
  
 這項工作由於資料和模型都是新的，您將要同時處理此結構和所有模型。  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>若要部署專案和處理所有採礦模型  
  
1.  在 **採礦模型**功能表上，選取**處理採礦結構和所有模型**。  
  
     如果您變更了結構，系統將會提示您建立及部署專案，然後才能處理模型。 按一下 [ **是**]。  
  
2.  按一下 [**執行**中**處理採礦結構 – 目標郵寄**] 對話方塊。  
  
     隨即開啟 **[處理進度]** 對話方塊，以顯示模型處理的詳細資料。 處理模型可能需要花一些時間，這會隨著您的電腦而不同。  
  
3.  在模型完成處理之後，按一下 **[處理進度]** 對話方塊中的 **[關閉]** 。  
  
4.  按一下 [**關閉**中**處理採礦結構 –\<結構 >** ] 對話方塊。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [將新模型加入至目標的郵寄結構&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：探索目標的郵寄模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [處理需求和考量 (資料採礦)](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
