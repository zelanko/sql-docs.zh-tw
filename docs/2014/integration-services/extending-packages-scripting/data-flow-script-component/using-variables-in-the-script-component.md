---
title: 在指令碼元件中使用變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d3ab6ce2bca61c7bdc78c66e157c2b00a9c5d664
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354716"
---
# <a name="using-variables-in-the-script-component"></a>在指令碼元件中使用變數
  變數會儲存封裝及其容器、工作與事件處理常式在執行階段所能使用的值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services-ssis-variables.md)。  
  
 您可以將現有的變數以唯讀或讀取/寫入存取自訂指令碼輸入以逗號分隔的清單中的變數`ReadOnlyVariables`並`ReadWriteVariables`欄位上**指令碼**頁面**指令碼轉換編輯器**。 請記住變數名稱有區分大小寫。 使用 `Value` 屬性讀取和寫入個別變數。 當指令碼在執行階段操作變數時，指令碼元件會在幕後處理任何所需的鎖定。  
  
> [!IMPORTANT]  
>  `ReadWriteVariables` 的集合只能在 `PostExecute` 方法中使用，才能最佳化效能並將鎖定衝突的風險降到最低。 因此您無法在處理每一列資料時，直接增量封裝變數值。 必須改增量區域變數值，並在處理所有的資料之後，將封裝變數值設定為 `PostExecute` 方法中的區域變數值。 您也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以解決這個限制，如本主題稍後所述。 不過，在處理每個資料列時直接寫入封裝變數，將會對效能產生負面的影響，並增加鎖定衝突的風險。  
  
 如需 [指令碼轉換編輯器] 之 [指令碼] 頁面的詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../script-transformation-editor-script-page.md)。  
  
 指令碼元件會在 `Variables` 專案項目中建立 `ComponentWrapper` 集合類別，它的每個預先設定的變數值 (屬性與變數本身的名稱相同) 都有強式類型的存取子屬性。 此集合是透過 `Variables` 類別的 `ScriptMain` 屬性來公開。 存取子屬性會提供適當的唯讀或是讀取/寫入權限給變數值。 例如，如果您已將名為 `MyIntegerVariable` 的整數變數加入 `ReadOnlyVariables` 清單，可以使用下列程式碼在指令碼中擷取其值：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 您也可以使用透過呼叫 `Me.VariableDispenser` 來存取的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以使用指令碼元件中的變數。 在這種情況下，您不是為變數使用具類型和具名的存取子屬性，而是直接存取變數。 在使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>時，您必須在自己的程式碼中處理變數值的鎖定語意和資料類型的轉換。 如果您想要使用在設計階段無法使用，但是會在執行階段以程式設計方式建立的變數，就必須使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，而不是具名與具類型的存取子屬性。  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services-ssis-variables.md)   
 [在封裝中使用變數](../../use-variables-in-packages.md)  
  
  
