---
title: 開發特定類型的資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0092a86412e5b9d33d53dbc79ff2c4770d8c10e4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354831"
---
# <a name="developing-specific-types-of-data-flow-components"></a>開發特定類型的資料流程元件
  本節涵蓋開發來源元件、具有同步輸出的轉換元件、具有非同步輸出的轉換元件以及目的地元件的細節。  
  
 如需元件開發的一般資訊，請參閱[開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [開發自訂來源元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 包含有關開發可從外部資料來源存取資料之元件的資訊，並將它提供給資料流程中的下游元件。  
  
 [開發具有同步輸出的自訂轉換元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 包含有關開發其輸出會同步到其輸入之轉換元件的資訊。 這些元件不會將資料加入資料流程，但是會在資料通過時處理它。  
  
 [開發具有非同步輸出的自訂轉換元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 包含有關開發其輸出不會同步到其輸入之轉換元件的資訊。 這些元件會從上游元件收到資料，但是也會將資料加入資料流程。  
  
 [開發自訂目的地元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 包含有關開發可從資料流程的上游元件收到資料列，並可將資料列寫入外部資料來源之元件的資訊。  
  
## <a name="reference"></a>參考資料  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 包含用以建立自訂資料流程元件的類別與介面。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 包含資料流程工作的 Unmanaged 類別與介面。 開發人員在以程式設計方式建立資料流程或是建立自訂資料流程元件時，使用這些以及 Managed <xref:Microsoft.SqlServer.Dts.Pipeline> 命名空間。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [比較指令碼解決方案和自訂物件](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [開發指令碼元件的特定類型](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
