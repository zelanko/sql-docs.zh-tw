---
title: "複製資料行轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3039b400b136b62840c40b463bb1d8f53a43251d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="copy-column-transformation"></a>複製資料行轉換
  「複製資料行」轉換會複製輸入資料行，並將新資料行加入轉換輸出，以建立新資料行。 稍後在資料流程中，可將不同的轉換套用至資料行副本。 例如，您可以使用「複製資料行」轉換建立資料行複本，然後使用「字元對應」轉換將複製的資料轉換為大寫字元，或使用「彙總」轉換將彙總套用至新資料行。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>設定複製資料行轉換  
 您可將輸入資料行指定為複製，以設定「複製資料行」轉換。 您可以在一個作業中建立資料行的多份副本，或是建立多個資料行的副本。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 **[複製資料行轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請參閱＜ [Copy Column Transformation Editor](../../../integration-services/data-flow/transformations/copy-column-transformation-editor.md)＞。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
