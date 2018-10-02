---
title: 將資料行對應到複合定義域 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2318f93e1bd8b5a11e14c17cb8b662db27b12fdf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728774"
---
# <a name="map-columns-to-composite-domains"></a>將資料行對應到複合定義域
  複合定義域是由兩個以上的單一定義域所組成。 您可以將多個資料行對應到定義域，也可將具有分隔值的單一資料行對應到定義域。  
  
 當您有多個資料行時，資料行必須個別對應到複合定義域中的每一個單一定義域，以將複合定義域規則套用於資料清理。 您將在 Data Quality Client 中選取複合定義域內所容納的單一定義域。 如需相關資訊，請參閱 [建立複合定義域](../../../data-quality-services/create-a-composite-domain.md)。  
  
 若為具有分隔值的單一資料行，則必須將該單一資料行對應到複合定義域。 各個值出現的順序務必與單一定義域出現在複合定義域中的順序相同。 資料來源中的分隔符號必須與用以剖析複合定義域值的分隔符號一致。 您將在 Data Quality Client 中為複合定義域選取分隔符號，並且設定其他屬性。 如需相關資訊，請參閱 [建立複合定義域](../../../data-quality-services/create-a-composite-domain.md)。  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>若要將多個資料行對應到複合定義域  
  
1.  以滑鼠右鍵按一下 DQS 清理轉換，然後按一下 [編輯]。  
  
2.  在 **[連接管理員]** 索引標籤上，確認複合定義域出現在可用的定義域清單中。  
  
3.  在 **[對應]** 索引標籤上，從 **[可用的輸入資料行]** 區域內選取資料行。  
  
4.  針對 **[輸入資料行]** 欄位中所列的每一個資料行，從 **[定義域]** 欄位中選取個別的單一定義域。 務必只選取位於複合定義域內的單一定義域。  
  
5.  視需要修改 **[來源別名]**、 **[輸出別名]** 和 **[狀態別名]** 欄位中所顯示的名稱。  
  
6.  視需要在 **[進階]** 索引標籤上設定屬性。如需這些屬性的詳細資訊，請參閱＜ [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md)＞。  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>若要將具有分隔值的資料行對應到複合定義網域  
  
1.  以滑鼠右鍵按一下 DQS 清理轉換，然後按一下 [編輯]。  
  
2.  在 **[連接管理員]** 索引標籤上，確認複合定義域出現在可用的定義域清單中。  
  
3.  在 **[對應]** 索引標籤上，從 **[可用的輸入資料行]** 區域內選取該資料行。  
  
4.  針對 **[輸入資料行]** 欄位中所列的資料行，從 **[定義域]** 欄位中選取複合定義域。  
  
5.  視需要修改 **[來源別名]**、 **[輸出別名]** 和 **[狀態別名]** 欄位中所顯示的名稱。  
  
6.  視需要在 **[進階]** 索引標籤上設定屬性。如需這些屬性的詳細資訊，請參閱＜ [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [DQS 清理轉換](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
