---
title: 合併轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 49e73b34167e7eb1b494995adce976ecf2601b22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="merge-transformation"></a>合併轉換
  「合併」轉換會將兩個已排序的資料集結合成單一資料集。 各資料集的資料列會根據其索引鍵資料行的值插入輸出中。  
  
 藉由在資料流程中加入「合併」轉換，即可執行下列工作：  
  
-   合併兩個資料來源的資料，例如資料表和檔案。  
  
-   藉由建立巢狀「合併」轉換，建立複雜的資料集。  
  
-   更正資料中的錯誤之後重新合併資料列。  
  
 「合併」轉換與「聯集全部」轉換類似。 在下列情況中，請使用「聯集全部」轉換取代「合併」轉換：  
  
-   轉換輸入未經排序時。  
  
-   結合的輸出不需要經過排序時。  
  
-   轉換擁有超過兩個輸入時。  
  
## <a name="input-requirements"></a>輸入需求  
 合併轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
 「合併」轉換也需要其輸入的合併資料行擁有相符的中繼資料。 例如，您無法合併數值資料類型的資料行，與字元資料類型的資料行。 如果資料是字串資料類型，第二個輸入中的資料行長度就必須小於或等於與其合併之第一個輸入中的資料行長度。  
  
 在 [ [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 中，「合併」轉換的使用者介面會自動對應擁有相同中繼資料的資料行。 您可接著手動對應其他擁有相容資料類型的資料行。  
  
 這個轉換有兩個輸入與一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-merge-transformation"></a>合併轉換的組態  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可以用程式設計的方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何設定屬性的詳細資訊，請參閱下列主題：  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>合併轉換編輯器
  使用 [合併轉換編輯器]，即可指定來自兩個已排序資料集的資料行，以進行合併。  
  
> [!IMPORTANT]  
>  合併轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
### <a name="options"></a>選項。  
 **輸出資料行名稱**  
 指定輸出資料行的名稱。  
  
 **合併輸入 1**  
 選取要合併為合併輸入 1 的資料行。  
  
 **合併輸入 2**  
 選取要合併為合併輸入 2 的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [合併聯結轉換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
