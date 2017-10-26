---
title: "資料列計數轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0eb554132024c6169f45fb24d739cb8f9f9d8caf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="row-count-transformation"></a>資料列計數轉換
  「資料列計數」轉換會在資料列通過資料流程時計算其數目，並將最後計數儲存到變數中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝可使用資料列計數更新指令碼、運算式和屬性運算式中使用的變數 (例如，儲存資料列計數的變數可更新電子郵件訊息中的訊息文字，以便加入資料列數)。「資料列計數」轉換使用的變數必須已存在，且必須在擁有「資料列計數」轉換的資料流程所屬的「資料流程」工作範圍內。  
  
 此轉換只會在最後一個資料列傳遞至轉換之後，才使用變數儲存資料列計數值。 因此，變數的值不會及時更新為使用資料流程中包含「資料列計數」轉換的更新值。 您可以在個別的資料流程中使用更新的變數。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-row-count-transformation"></a>資料列計數轉換的組態  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

