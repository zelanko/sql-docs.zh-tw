---
title: "多點傳送轉換 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.multicasttrans.f1"
helpviewer_keywords: 
  - "多個輸出"
  - "多點傳送轉換"
  - "資料集 [Integration Services], 多個輸出"
  - "多個轉換"
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# 多點傳送轉換
  「多點傳送」轉換會將其輸入散發至一個或多個輸出。 此轉換與「條件式分割」轉換類似。 這兩種轉換都會將輸入導向多個輸出， 兩者的差異在於「多點傳送」轉換會將每個資料列導向每個輸出，而「條件式分割」會將一個資料列導向單一輸出。 如需詳細資訊，請參閱 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
 您可加入輸出以設定「多點傳送」轉換。  
  
 使用「多點傳送」轉換時，封裝可建立資料的邏輯副本。 當封裝需要將多組轉換套用至相同資料時，此功能會很有用。 例如，彙總一份資料副本且只將摘要資訊載入其目的地，但是以查閱值和衍生的資料行擴充另一份資料副本，再將其載入目的地。  
  
 此轉換有一個輸入和多個輸出， 它不支援錯誤輸出。  
  
## 設定多點傳送轉換  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可在 **[多點傳送轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請參閱＜ [Multicast Transformation Editor](../../../integration-services/data-flow/transformations/multicast-transformation-editor.md)＞。  
  
 如需有關可以程式設計方式設定之屬性的詳細資訊，請參閱＜ [Common Properties](../Topic/Common%20Properties.md)＞。  
  
## 相關工作  
 如需如何設定此元件屬性的資訊，請參閱[設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## 請參閱＜  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  