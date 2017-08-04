---
title: "增強錯誤輸出 with the Script Component |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 3881b57f4089dbb075d019f9bd1a88a96a307b72
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="enhancing-an-error-output-with-the-script-component"></a>使用指令碼元件增強錯誤輸出
  根據預設，在兩個額外的資料行[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]錯誤輸出，ErrorCode 與 ErrorColumn 只包含數字碼，代表錯誤號碼及發生錯誤的資料行的識別碼。 這些數字的值可能是沒有對應的錯誤描述和資料行名稱，則用途有限。  
  
 本主題描述如何使用指令碼元件將錯誤描述和資料行名稱加入至資料流程中的現有錯誤輸出資料。 此範例使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法 (可透過指令碼元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 屬性取得)，加入對應至特定預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼之錯誤描述。 此範例將擷取的歷程識別碼對應的資料行名稱使用<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>相同介面的方法。  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>範例  
 如下所示的範例會使用指令碼元件設定成轉換，將錯誤描述和資料行名稱加入至資料流程中的現有錯誤輸出資料。  
  
 如需如何設定使用的指令碼元件為資料流程中的資料轉換的詳細資訊，請參閱[使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用指令碼元件建立非同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  在建立新指令碼元件之前，請先設定資料流程中的上游元件，使它在錯誤或截斷發生時將資料列重新導向至其錯誤輸出。 為了進行測試，您可能會想要以確定錯誤將發生的方式設定元件，例如，在查閱將失敗的兩個資料表之間，設定「查閱」轉換。  
  
2.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
3.  從上游元件將錯誤輸出連接至新指令碼元件。  
  
4.  開啟**指令碼轉換編輯器**，然後在**指令碼** 頁面上，針對**ScriptLanguage**屬性，選取指令碼語言。  
  
5.  按一下**編輯指令碼**開啟[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 加入如下所示的範例程式碼。  
  
6.  關閉 VSTA。  
  
7.  在指令碼轉換編輯器中，在**的輸入資料行**頁面上，選取 ErrorCode 和 ErrorColumn 資料行。  
  
8.  在**輸入和輸出**頁面上，新增兩個新的資料行。  
  
    -   加入新的輸出資料行型別的**字串**名為**ErrorDescription**。 將新資料行的預設長度增加至 255，以支援長訊息。  
  
    -   加入另一個新的輸出資料行型別的**字串**名為**ColumnName**。 預設長度增加至 255，以支援長值的新資料行。  
  
9. 關閉**指令碼轉換編輯器。**  
  
10. 將指令碼元件的輸出附加至適當的目的地。 一般檔案目的地對於特定測試而言是最容易設定的。  
  
11. 執行封裝。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
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
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)   
 [在資料流程元件中使用錯誤輸出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
