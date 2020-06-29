---
title: 多點傳送轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b5c0a38c966c89f426a213f302b45c390b77cfe
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437605"
---
# <a name="multicast-transformation"></a>多點傳送轉換
  「多點傳送」轉換會將其輸入散發至一個或多個輸出。 此轉換與「條件式分割」轉換類似。 這兩種轉換都會將輸入導向多個輸出， 兩者的差異在於「多點傳送」轉換會將每個資料列導向每個輸出，而「條件式分割」會將一個資料列導向單一輸出。 如需詳細資訊，請參閱 [Conditional Split Transformation](conditional-split-transformation.md)。  
  
 您可加入輸出以設定「多點傳送」轉換。  
  
 使用「多點傳送」轉換時，封裝可建立資料的邏輯副本。 當封裝需要將多組轉換套用至相同資料時，此功能會很有用。 例如，彙總一份資料副本且只將摘要資訊載入其目的地，但是以查閱值和衍生的資料行擴充另一份資料副本，再將其載入目的地。  
  
 此轉換有一個輸入和多個輸出， 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-multicast-transformation"></a>設定多點傳送轉換  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 **[多點傳送轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請參閱＜ [Multicast Transformation Editor](../../multicast-transformation-editor.md)＞。  
  
 如需有關可以程式設計方式設定之屬性的詳細資訊，請參閱＜ [Common Properties](../../common-properties.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
