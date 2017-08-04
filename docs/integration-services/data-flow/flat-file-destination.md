---
title: "一般檔案目的地 |Microsoft 文件"
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
- sql13.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 78a0ec526f83dcab8d7358ef5a51f1f6ccfd0a04
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-destination"></a>一般檔案目的地
  「一般檔案」目的地會將資料寫入文字檔。 該文字檔的格式可以是使用分隔符號、固定寬度、具有資料列分隔符號的固定寬度，或不齊右。  
  
 您可以利用下列方式設定「一般檔案」目的地：  
  
-   提供寫入任何資料前插入到檔案的文字區塊。 該文字可提供如資料行標題等資訊。  
  
-   指定是否覆寫同名目的地檔案中的資料。  
  
 此目的地使用「一般檔案」連接管理員來存取文字檔。 透過設定「一般檔案」目的地使用之「一般檔案」連接管理員上的屬性，您可以指定「一般檔案」目的地如何格式化並寫入文字檔。 設定「一般檔案」連接管理員時，可以指定有關該檔案以及檔案中每一資料行的資訊。 例如，指定分隔檔案中資料行和資料列的字元，以及各資料行的資料類型和長度。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 一般檔案目的地包含 [標頭] 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)和[一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)。  
  
 此目的地擁有一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-flat-file-destination"></a>一般檔案目的地的組態  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關 **[一般檔案來源編輯器]** 對話方塊中可設定屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [一般檔案目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/flat-file-destination-editor-connection-manager-page.md)  
  
-   [一般檔案目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定資料流程元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [一般檔案來源](../../integration-services/data-flow/flat-file-source.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
