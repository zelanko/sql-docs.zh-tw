---
title: 啟用採礦模型的鑽取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ce3967bf9258e9b8f6cd4a28cb28a29a1e0588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084536"
---
# <a name="enable-drillthrough-for-a-mining-model"></a>針對採礦模型啟用鑽研
  如果您已經啟用採礦模型的鑽研，當您瀏覽此模型時，可以擷取有關用來建立模型之案例的詳細資訊。 若要檢視這項資訊，您必須擁有必要的權限，而且結構必須已經經過處理。  
  
 **許可權**若要讓使用者深入瞭解模型資料或結構資料，使用者必須是具有採礦模型或採礦結構之[AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl)許可權的角色成員。 鑽研權限是在結構和模型上分別設定的。  
  
-   即使您沒有結構的權限，模型的鑽研權限還是可以讓您從模型進行鑽研。  
  
-   結構的鑽研權限可以使用 [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 函數，提供將結構資料行從模型加入到鑽研查詢的額外功能。 您也可以使用 [選取 ...] 來查詢結構中的定型和測試案例。FROM \<結構>。案例語法。  
  
 **定型案例的**快取「抓取」的運作方式是藉由在採礦結構中抓取定型案例的相關資訊。 這項資訊會在處理結構時快取。 因此，如果您選擇將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 `ClearAfterProcessing` 來清除所有快取的資料，鑽研將不會運作。  
  
> [!NOTE]  
>  如果尚未快取定型案例，您必須將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 **KeepTrainingCases** ，然後在可以檢視案例資料之前，重新處理模型。  
  
 如需詳細資訊，請參閱[鑽研查詢 &#40;資料採礦&#41;](drillthrough-queries-data-mining.md)。  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>針對採礦模型啟用鑽研  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師的 [採礦模型]**** 索引標籤上，以滑鼠右鍵按一下您想要啟用鑽研之採礦模型的名稱，然後選取 [屬性]****。  
  
2.  在 [屬性]**** 視窗中，按一下 [AllowDrillThrough]****，然後選取 [True]****。  
  
3.  在 [採礦模型]**** 索引標籤中，以滑鼠右鍵按一下模型，然後選取 [處理模型]****。  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>針對採礦結構啟用快取  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師的 [採礦結構]**** 索引標籤上，以滑鼠右鍵按一下採礦結構的名稱。  
  
2.  開啟 [屬性]**** 視窗。  
  
3.  在 [屬性]**** 視窗中，找出 **CacheMode** 屬性，然後從清單中選取 [KeepTrainingCases]****。  
  
4.  在 [資料庫]**** 功能表中，選取 [處理]****。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦&#41;&#40;的鑽取查詢](drillthrough-queries-data-mining.md)  
  
  
