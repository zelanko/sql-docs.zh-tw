---
title: 在指令碼元件中使用變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 51dddf0e5fd971aeb2aa1229bb1af2faae744b6e
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51638525"
---
# <a name="using-variables-in-the-script-component"></a>在指令碼元件中使用變數
  變數會儲存封裝及其容器、工作與事件處理常式在執行階段所能使用的值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)。  
  
 您可以在 [指令碼轉換編輯器] 的 [指令碼] 頁面上的 [ReadOnlyVariables] 與 [ReadWriteVariables] 欄位中輸入以逗號分隔的變數清單，來將現有的變數以唯讀或讀取/寫入存取的方式提供自訂指令碼使用。 請記住變數名稱有區分大小寫。 使用 **Value** 屬性讀取和寫入個別變數。 當指令碼在執行階段操作變數時，指令碼元件會在幕後處理任何所需的鎖定。  
  
> [!IMPORTANT]  
>  **ReadWriteVariables** 的集合只能在 **PostExecute** 方法中使用，才能最佳化效能並將鎖定衝突的風險降到最低。 因此您無法在處理每一列資料時，直接增量封裝變數值。 請改為遞增區域變數值，並在處理所有的資料之後，將封裝變數值設定為 **PostExecute** 方法中的區域變數值。 您也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以解決這個限制，如本主題稍後所述。 不過，在處理每個資料列時直接寫入封裝變數，將會對效能產生負面的影響，並增加鎖定衝突的風險。  
  
 如需 [指令碼轉換編輯器] 之 [指令碼] 頁面的詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)。  
  
 指令碼元件會在 **ComponentWrapper** 專案項目中建立 **Variables** 集合類別，並針對每個預先設定的變數值提供一個強型別存取子屬性 (其名稱與變數本身的名稱相同)。 此集合是透過 **ScriptMain** 類別的 **Variables** 屬性來公開。 存取子屬性會提供適當的唯讀或是讀取/寫入權限給變數值。 例如，如果您已將名為 `MyIntegerVariable` 的整數變數加入 [ReadOnlyVariables] 清單，可以使用下列程式碼在指令碼中擷取其值：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 您也可以使用透過呼叫 `Me.VariableDispenser` 來存取的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以使用指令碼元件中的變數。 在這種情況下，您不是為變數使用具類型和具名的存取子屬性，而是直接存取變數。 在使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>時，您必須在自己的程式碼中處理變數值的鎖定語意和資料類型的轉換。 如果您想要使用在設計階段無法使用，但是會在執行階段以程式設計方式建立的變數，就必須使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，而不是具名與具類型的存取子屬性。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)   
 [在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
