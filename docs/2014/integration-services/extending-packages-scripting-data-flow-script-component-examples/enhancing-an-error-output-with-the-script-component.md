---
title: 使用指令碼元件增強錯誤輸出 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dd935387e8d6e4a95a25d21eb5d5d229f9599bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62895487"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>使用指令碼元件增強錯誤輸出
  依預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤輸出中的兩個額外資料行 ErrorCode 與 ErrorColumn 只包含數字碼，代表錯誤號碼及發生錯誤之資料行的識別碼。 這些數值若無對應的錯誤描述，則用途有限。  
  
 此主題描述如何使用指令碼元件，將錯誤描述資料行加入資料流程中的現有錯誤輸出資料。 此範例使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 方法 (可透過指令碼元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性取得)，加入對應至特定預先定義的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 錯誤碼之錯誤描述。  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>範例  
 在這裡顯示的範例使用設定成轉換的指令碼元件，將錯誤描述資料行加入資料流程中的現有錯誤輸出資料。  
  
 如需如何設定腳本元件做為資料流程中的轉換的詳細資訊，請參閱[使用腳本元件建立同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用腳本元件建立異步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  在建立新指令碼元件之前，請先設定資料流程中的上游元件，使它在錯誤或截斷發生時將資料列重新導向至其錯誤輸出。 為了進行測試，您可能會想要以確定錯誤將發生的方式設定元件，例如，在查閱將失敗的兩個資料表之間，設定「查閱」轉換。  
  
2.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
3.  從上游元件將錯誤輸出連接至新指令碼元件。  
  
4.  開啟**指令碼轉換編輯器**，然後在 [指令碼]**** 頁面上選取 **ScriptLanguage** 屬性的指令碼語言。  
  
5.  按一下 [編輯指令碼]**** 開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，並新增以下所示的範例程式碼。  
  
6.  關閉 VSTA。  
  
7.  在 [腳本轉換編輯器] 的 [**輸入資料行**] 頁面上，選取 [ErrorCode] 資料行。  
  
8.  在 [**輸入和輸出**] 頁面上，加入名為**ErrorDescription**之`String`類型的新輸出資料行。 將新資料行的預設長度增加至 255，以支援長訊息。  
  
9. 關閉**指令碼轉換編輯器**。  
  
10. 將指令碼元件的輸出附加至適當的目的地。 一般檔案目的地對於特定測試而言是最容易設定的。  
  
11. 執行封裝。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  Row.ErrorDescription = _  
    Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
  Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
    }  
}  
  
```  
  
![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [資料中的錯誤處理](../data-flow/error-handling-in-data.md)   
 [在資料流程元件中使用錯誤輸出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用指令碼元件建立同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
