---
title: "開發特定類型的資料流程元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0d0d2fc6d14ee2c597957ba8c660d4e341ae1215
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="developing-specific-types-of-data-flow-components"></a>開發特定類型的資料流程元件
  本節涵蓋開發來源元件、具有同步輸出的轉換元件、具有非同步輸出的轉換元件以及目的地元件的細節。  
  
 如需開發一般情況下，請參閱[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [開發自訂來源元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 包含有關開發可從外部資料來源存取資料之元件的資訊，並將它提供給資料流程中的下游元件。  
  
 [開發具有同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 包含有關開發其輸出會同步到其輸入之轉換元件的資訊。 這些元件不會將資料加入資料流程，但是會在資料通過時處理它。  
  
 [開發具有非同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 包含有關開發其輸出不會同步到其輸入之轉換元件的資訊。 這些元件會從上游元件收到資料，但是也會將資料加入資料流程。  
  
 [開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 包含有關開發可從資料流程的上游元件收到資料列，並可將資料列寫入外部資料來源之元件的資訊。  
  
## <a name="reference"></a>參考  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 包含用以建立自訂資料流程元件的類別與介面。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 包含資料流程工作的 Unmanaged 類別與介面。 開發人員在以程式設計方式建立資料流程或是建立自訂資料流程元件時，使用這些以及 Managed <xref:Microsoft.SqlServer.Dts.Pipeline> 命名空間。  
  
## <a name="see-also"></a>另請參閱  
 [比較指令碼方案和自訂物件](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [開發指令碼元件的特定類型](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  

