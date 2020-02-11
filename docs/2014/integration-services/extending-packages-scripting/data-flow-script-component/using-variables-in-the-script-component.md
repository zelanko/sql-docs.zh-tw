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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 922454c7bc04a211d6f54754d48331fdfdffeb07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894967"
---
# <a name="using-variables-in-the-script-component"></a>在指令碼元件中使用變數
  變數會儲存封裝及其容器、工作與事件處理常式在執行階段所能使用的值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services-ssis-variables.md)。  
  
 您可以`ReadOnlyVariables`在 [**腳本轉換編輯器**] 的 [**腳本**] 頁面上，于和欄位中輸入以逗號分隔的變數清單， `ReadWriteVariables`讓現有的變數可供自訂腳本進行唯讀或讀取/寫入存取。 請記住變數名稱有區分大小寫。 使用 `Value` 屬性讀取和寫入個別變數。 當指令碼在執行階段操作變數時，指令碼元件會在幕後處理任何所需的鎖定。  
  
> [!IMPORTANT]  
>  
  `ReadWriteVariables` 的集合只能在 `PostExecute` 方法中使用，才能最佳化效能並將鎖定衝突的風險降到最低。 因此您無法在處理每一列資料時，直接增量封裝變數值。 必須改增量區域變數值，並在處理所有的資料之後，將封裝變數值設定為 `PostExecute` 方法中的區域變數值。 您也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，以解決這個限制，如本主題稍後所述。 不過，在處理每個資料列時直接寫入封裝變數，將會對效能產生負面的影響，並增加鎖定衝突的風險。  
  
 如需 [指令碼轉換編輯器]  之 [指令碼]  頁面的詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../script-transformation-editor-script-page.md)。  
  
 指令碼元件會在 `Variables` 專案項目中建立 `ComponentWrapper` 集合類別，它的每個預先設定的變數值 (屬性與變數本身的名稱相同) 都有強式類型的存取子屬性。 此集合是透過 `Variables` 類別的 `ScriptMain` 屬性來公開。 存取子屬性會提供適當的唯讀或是讀取/寫入權限給變數值。 例如，如果您已將名為 `MyIntegerVariable` 的整數變數加入 `ReadOnlyVariables` 清單，可以使用下列程式碼在指令碼中擷取其值：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 您也可以使用透過呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 來存取的 `Me.VariableDispenser` 屬性，以使用指令碼元件中的變數。 在這種情況下，您不是為變數使用具類型和具名的存取子屬性，而是直接存取變數。 在使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>時，您必須在自己的程式碼中處理變數值的鎖定語意和資料類型的轉換。 如果您想要使用在設計階段無法使用，但是會在執行階段以程式設計方式建立的變數，就必須使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 屬性，而不是具名與具類型的存取子屬性。  
  
![Integration Services 圖示（小型）](../../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services-ssis-variables.md)   
 [在套件中使用變數](../../use-variables-in-packages.md)  
  
  
