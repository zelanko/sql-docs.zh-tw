---
title: 將羅吉斯迴歸模型加入到撥接中心結構 （中繼資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ccadf7665b112b6ba1055fdcf69aeb99609c3ab3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312426"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>將羅吉斯迴歸模型加入到撥接中心結構 (中繼資料採礦教學課程)
  除了分析可能會影響撥接中心作業的因數之外，您還必須提供有關員工如何改進服務品質的一些特定建議。 在這個工作中，您將使用和探勘模型相同的採礦結構，並加入一個採礦模型用於建立預測。  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，羅吉斯迴歸模型是以類神經網路演算法為基礎，因此與類神經網路模型提供相同的彈性和功能。 不過，羅吉斯迴歸演算法特別適合用來預測二進位結果。  
  
 在這個案例中，您將使用類神經網路模型所用的相同採礦結構。 不過，您將針對您的商務問題自訂新的模型。 您對改進服務品質及判斷所需的資深操作員人數特別感興趣，因此將設定模型以預測這些值。  
  
 為了確保以撥接中心資料為基礎的所有模型盡可能相似，您將使用和以前相同的初始值。 設定種子參數可確保模型會從相同起點開始處理資料，將資料中的成品所造成的變化降至最低。  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>將新的採礦模型加入到撥接中心採礦結構中  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在 [方案總管] 中，以滑鼠右鍵按一下採礦結構中，**呼叫 Center 分類收納**，然後選取**開啟設計工具**。  
  
2.  在 資料採礦設計師中，按一下 **採礦模型** 索引標籤。  
  
3.  按一下**建立相關的採礦模型**。  
  
4.  在**新增採礦模型**對話方塊中，針對**模型名稱**，型別`Call Center - LR`。  如**演算法名稱**，選取**Microsoft 羅吉斯迴歸**。  
  
5.  按一下 [確定] 。  
  
     新的採礦模型會顯示在**採礦模型** 索引標籤。  
  
### <a name="to-customize-the-logistic-regression-model"></a>自訂羅吉斯迴歸模型  
  
1.  在新的採礦模型的資料行`Call Center - LR`，將 Fact CallCenter ID 做為索引鍵。  
  
2.  變更值 ServiceGrade 和 「 二級操作員以**預測**。  
  
     這些資料行將同時用於輸入和預測。 基本上，您是在相同的資料上建立兩個不同的模型：一個用來預測操作員人數，一個用來預測服務等級。  
  
3.  變更所有其他資料行，**輸入**。  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>指定種子和處理模型  
  
1.  在**採礦模型**索引標籤，以滑鼠右鍵按一下資料行的模型為撥接中心-LR，然後選取**設定演算法參數**。  
  
2.  在 HOLDOUT_SEED 參數的資料列，請按一下底下的空資料格**值**，然後輸入`1`。 按一下 [確定] 。  
  
    > [!NOTE]  
    >  只要您將相同的種子用於所有相關的模型，您選擇做為種子的值就不重要了。  
  
3.  在**採礦模型**功能表上，選取**處理採礦結構和所有模型**。 按一下**是**將更新的資料採礦專案部署到伺服器。  
  
4.  在**處理採礦模型**對話方塊中，按一下 **執行**。  
  
5.  按一下**關閉**關閉**處理進度**對話方塊，然後按一下**關閉**中再次**處理採礦模型** 對話方塊。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立用於撥接中心模型的預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [處理需求和考量&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  