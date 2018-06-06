---
title: 設定資料行的資料類型 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18aa18d9c9ee7fbc0291d9961e144263053710dd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="set-the-data-type-of-a-column"></a>設定資料行的資料類型 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  當您將資料匯入或貼上模型時，模型設計師會自動偵測並套用資料類型。 將資料加入至模型之後，您可以手動修改資料行的資料類型，以變更資料儲存的方式。 如果您只要變更資料顯示方式的格式，而不要變更其儲存方式，可以只變更該顯示格式。  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>若要變更資料行的資料類型或顯示格式  
  
1.  在模型設計師中，選取您要變更資料類型或顯示格式的資料行。  
  
2.  在資料行 **[屬性]** 視窗中，執行下列其中一項：  
  
    -   在 **[資料格式]** 屬性中，選取其他資料格式。  
  
    -   在 **[資料類型]** 屬性中，選取其他資料類型。  
  
## <a name="considerations-when-changing-data-types"></a>變更資料類型時的考量  
 有時當您嘗試變更資料行的資料類型或選取資料轉換時，可能會發生下列其中一項錯誤：  
  
-   無法變更資料類型  
  
-   無法變更資料行資料類型  
  
 即使該資料類型以選項的形式出現在 [資料類型] 下拉式清單中提供使用，也可能會發生這些錯誤。 本節將說明這些錯誤的原因及更正方法。  
  
### <a name="understanding-automatically-determined-data-types"></a>了解自動判斷的資料類型  
 當您將資料加入至模型時，模型設計師會檢查資料的資料行，以查看每個資料行所包含的資料類型。 如果該資料行中的資料是一致的，就會指派最精確的資料類型至該資料行。  
  
 但是，如果加入的資料是來自 Excel 或其他不強制在每個資料行內使用單一資料類型的來源時，模型設計師將指派可適合此資料行內所有值的資料類型。 因此，如果資料行包含不同類型的數字 (如整數、長數字和貨幣)，模型設計師會使用十進位資料類型。 或者，如果資料行中混合數字和文字，則模型設計師會使用文字資料類型。 模型設計師不提供與 Excel「通用格式」資料類型類似的資料類型。  
  
 因此，如果資料行同時包含數字和文字值，您便無法將此資料行轉換成數值資料類型。  
  
 下列是商業智慧語意模型中可用的資料類型：  
  
-   **文字**  
  
-   **十進位數字**  
  
-   **整數**  
  
-   **貨幣**  
  
-   **TRUE/FALSE**  
  
-   **日期**  
  
 如果發現資料的資料類型錯誤，或是與您想要的資料類型不同，您有幾個選擇：  
  
-   您可以重新匯入資料。 若要重新匯入，請開啟與資料來源之間的現有連接，然後重新匯入資料行。 根據資料來源類型而定，您也許可以在匯入期間套用篩選來移除有問題的值。  
  
-   您可以在導出資料行中建立 DAX 公式來建立屬於所需資料類型的新值 例如，可以使用 TRUNC 函數將十進位數字變更為整數，或者可以結合資訊函數和邏輯函數來測試及轉換值。  
  
### <a name="understanding-data-conversion"></a>了解資料轉換  
 如果您在選取資料轉換選項時發生錯誤，可能是目前資料行的資料類型不支援所選取的轉換。 並非所有資料類型都允許所有轉換。 例如，如果目前資料行的資料類型為數字 (整數或十進位) 或文字，您只能將資料行變更為布林值資料類型。 因此，您必須針對資料行中的資料選擇適當的資料類型。  
  
 當您選擇適當的資料類型之後，模型設計師會警告您可能發生的資料變更，例如失去精確度或截斷。 請按一下 [確定] 接受，然後將資料變更為新的資料類型。  
  
 如果資料類型受到支援，但是模型設計師卻發現不受新資料類型支援的值，您會接到另一項錯誤，並將需要修正資料值，才能再繼續進行。  
  
 如需使用商業智慧語意模型中的資料類型的詳細資訊，它們都是隱含轉換以及不同資料類型的方式公式中使用，請參閱[支援的資料類型](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)。  
  
## <a name="see-also"></a>另請參閱  
 [支援的資料類型](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)  
  
  
