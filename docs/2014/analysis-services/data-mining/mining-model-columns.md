---
title: 採礦模型資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f99a2dc218543faa4d862fa7520c1618ec307ba7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083710"
---
# <a name="mining-model-columns"></a>採礦模型資料行
  資料採礦模型會將採礦模型演算法套用至以採礦結構表示的資料。 與採礦結構相同，採礦模型也會包含資料行。 採礦模型包含在採礦結構內，且繼承採礦結構所定義的所有屬性值。 此模型可以使用採礦結構包含的所有資料行或資料行子集。  
  
 您可以在採礦模型資料行上定義兩項額外資訊：使用方式和模型旗標。  
  
-   **使用**方式是定義模型如何使用資料行的屬性。 資料行可以做為輸入資料行、索引鍵資料行或可預測資料行使用。  
  
-   **模型旗標**會提供演算法，其中包含案例資料表中所定義資料的其他資訊，讓演算法可以建立更精確的模型。 您可以使用資料採礦延伸模組 (DMX) 語言以程式設計方式定義模型旗標，或在 ** 的 [資料採礦設計師]**[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中定義。  
  
 下列清單描述您在採礦模型資料行上可以定義的模型旗標。  
  
 `MODEL_EXISTENCE_ONLY`  
 指出屬性是否出現比屬性資料行中的值更重要。 例如，假設案例資料表包含與特定客戶相關聯的訂購項目清單。 資料表資料包含每一個項目的產品類型、識別碼以及成本。 針對模型的用途而言，客戶購買特定訂購項目的事實可能比訂購項目本身的成本更重要。 在此情況下，成本資料行應該標示為 `MODEL_EXISTENCE_ONLY`。  
  
 `REGRESSOR`  
 指示演算法可以在迴歸演算法的迴歸公式中使用指定的資料行。 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法支援此旗標。  
  
 如需使用 DMX 以程式設計方式設定 Usage 屬性以及定義模型旗標的詳細資訊，請參閱 [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)。 如需在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中設定 Usage 屬性以及定義模型旗標的詳細資訊，請參閱 [移動資料採礦物件](moving-data-mining-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;Analysis Services 的採礦結構-資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [變更採礦模型的屬性](change-the-properties-of-a-mining-model.md)   
 [從採礦模型中排除資料行](exclude-a-column-from-a-mining-model.md)   
 [採礦結構資料行](mining-structure-columns.md)  
  
  
