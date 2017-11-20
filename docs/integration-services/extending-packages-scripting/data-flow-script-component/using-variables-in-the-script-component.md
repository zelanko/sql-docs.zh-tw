---
title: "在指令碼元件中使用變數 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>在指令碼元件中使用變數
  變數會儲存封裝及其容器、工作與事件處理常式在執行階段所能使用的值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)。  
  
 您可以將現有的變數可供唯讀或讀取/寫入存取的自訂指令碼輸入以逗號分隔清單中的變數**[readonlyvariables]**和**[readwritevariables]**欄位上**指令碼**頁面**指令碼轉換編輯器**。 請記住變數名稱有區分大小寫。 使用**值**讀取和寫入個別變數的屬性。 當指令碼在執行階段操作變數時，指令碼元件會在幕後處理任何所需的鎖定。  
  
> [!IMPORTANT]  
>  集合**[readwritevariables]**僅供以**PostExecute**方法來將效能最大化，並鎖定衝突的風險降至最低。 因此您無法在處理每一列資料時，直接增量封裝變數值。 相反地，將本機變數的值遞增，並設定封裝變數的值為本機變數中的值**PostExecute**經過處理之後的所有資料的方法。 您也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以解決這個限制，如本主題稍後所述。 不過，在處理每個資料列時直接寫入封裝變數，將會對效能產生負面的影響，並增加鎖定衝突的風險。  
  
 如需有關**指令碼**頁面**指令碼轉換編輯器**，請參閱[設定指令碼元件指令碼元件編輯器中](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;指令碼頁面 &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 指令碼元件建立**變數**中的集合類別**ComponentWrapper**強型別存取子屬性的值與每個預先設定變數之屬性具有相同名稱與變數本身的專案項目。 此集合會公開透過**變數**屬性**ScriptMain**類別。 存取子屬性會提供適當的唯讀或是讀取/寫入權限給變數值。 例如，如果您已經加入整數變數，名為`MyIntegerVariable`至**readonlyvariables**  清單中，您可以擷取其值在您的指令碼中使用下列程式碼：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 您也可以使用透過呼叫 `Me.VariableDispenser` 來存取的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以使用指令碼元件中的變數。 在這種情況下，您不是為變數使用具類型和具名的存取子屬性，而是直接存取變數。 在使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>時，您必須在自己的程式碼中處理變數值的鎖定語意和資料類型的轉換。 如果您想要使用在設計階段無法使用，但是會在執行階段以程式設計方式建立的變數，就必須使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，而不是具名與具類型的存取子屬性。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;變數](../../../integration-services/integration-services-ssis-variables.md)   
 [在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

