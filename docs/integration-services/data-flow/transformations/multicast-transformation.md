---
title: 多點傳送轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
- sql13.dts.designer.multicasttransformation.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 795eacbaacc5fca1cc3d51908a365986019543c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664966"
---
# <a name="multicast-transformation"></a>多點傳送轉換
  「多點傳送」轉換會將其輸入散發至一個或多個輸出。 此轉換與「條件式分割」轉換類似。 這兩種轉換都會將輸入導向多個輸出， 兩者的差異在於「多點傳送」轉換會將每個資料列導向每個輸出，而「條件式分割」會將一個資料列導向單一輸出。 如需詳細資訊，請參閱 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
 您可加入輸出以設定「多點傳送」轉換。  
  
 使用「多點傳送」轉換時，封裝可建立資料的邏輯副本。 當封裝需要將多組轉換套用至相同資料時，此功能會很有用。 例如，彙總一份資料副本且只將摘要資訊載入其目的地，但是以查閱值和衍生的資料行擴充另一份資料副本，再將其載入目的地。  
  
 此轉換有一個輸入和多個輸出， 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-multicast-transformation"></a>設定多點傳送轉換  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以程式設計方式設定之屬性的詳細資訊，請參閱＜ [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)＞。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="multicast-transformation-editor"></a>多點傳送轉換編輯器
  使用 **[多點傳送轉換編輯器]** 對話方塊檢視和設定每個轉換輸出的屬性。  
  
### <a name="options"></a>選項。  
 **輸出**  
 在左方選取輸出，即可在右方檢視其在資料表中的屬性。  
  
 **屬性**  
 除了 [名稱] 和 [描述] 以外，所有列出的輸出屬性都是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
