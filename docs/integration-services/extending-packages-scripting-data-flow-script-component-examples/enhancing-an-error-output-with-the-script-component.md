---
description: 使用指令碼元件增強錯誤輸出
title: 使用指令碼元件增強錯誤輸出 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e6150c8b80b29575cbb08c4cd88ebe342a55da79
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123033"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>使用指令碼元件增強錯誤輸出

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  根據預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤輸出中的兩個額外資料行 ErrorCode 和 ErrorColumn 只包含數字碼，代表錯誤號碼及發生錯誤之資料行的識別碼。 這些數值若無對應的錯誤描述和資料行名稱，則用途有限。  
  
 此主題描述如何使用指令碼元件，將錯誤描述和資料行名稱新增至資料流程現有的錯誤輸出資料。 此範例使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法 (可透過指令碼元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 屬性取得)，加入對應至特定預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼之錯誤描述。 然後，本例會使用相同介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> 方法新增資料行名稱，此名稱對應至擷取的歷程識別碼。  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>範例  
 在這裡顯示的範例使用設定成轉換的指令碼元件，將錯誤描述和資料行名稱新增至資料流程現有的錯誤輸出資料。  
  
 如需如何設定指令碼元件以用作資料流程中轉換的詳細資訊，請參閱[使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用指令碼元件建立非同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  在建立新指令碼元件之前，請先設定資料流程中的上游元件，使它在錯誤或截斷發生時將資料列重新導向至其錯誤輸出。 為了進行測試，您可能會想要以確定錯誤將發生的方式設定元件，例如，在查閱將失敗的兩個資料表之間，設定「查閱」轉換。  
  
2.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
3.  從上游元件將錯誤輸出連接至新指令碼元件。  
  
4.  開啟 **指令碼轉換編輯器**，然後在 [指令碼] 頁面上選取 **ScriptLanguage** 屬性的指令碼語言。  
  
5.  按一下 [編輯指令碼] 以開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，並新增以下所示的範例程式碼。  
  
6.  關閉 VSTA。  
  
7.  在指令碼轉換編輯器的 [輸入資料行] 頁面上，選取 ErrorCode 和 ErrorColumn 資料行。  
  
8.  在 [輸入及輸出] 頁面上新增兩個新的資料行。  
  
    -   新增新的輸出資料行，類型為 **字串** 名稱為 **ErrorDescription**。 將新資料行的預設長度增加至 255，以支援長訊息。  
  
    -   新增另一個新的輸出資料行，類型為 **字串**，名稱為 **ColumnName**。 將新資料行的預設長度增加至 255，以支援長值。  
  
9. 關閉 **指令碼轉換編輯器**。  
  
10. 將指令碼元件的輸出附加至適當的目的地。 一般檔案目的地對於特定測試而言是最容易設定的。  
  
11. 執行封裝。  

```vb
Public Class ScriptMain      ' VB
    Inherits UserComponent
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)

        Row.ErrorDescription = _
            Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)

        Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)

        If componentMetaData130 IsNot Nothing Then

            If Row.ErrorColumn = 0 Then
                ' 0 means no specific column is identified by ErrorColumn, this time.
                Row.ColumnName = "Check the row for a violation of a foreign key constraint."
            ELSE If Row.ErrorColumn = -1 Then
                ' -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables."
            Else
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)
            End If
        End If
    End Sub
End Class
```

```csharp
public class ScriptMain:      // C#
    UserComponent
{
    public override void Input0_ProcessInputRow(Input0Buffer Row)
    {
        Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);

        var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;
        if (componentMetaData130 != null)
        {
            // 0 means no specific column is identified by ErrorColumn, this time.
            if (Row.ErrorColumn == 0)
            {
                Row.ColumnName = "Check the row for a violation of a foreign key constraint.";
            }
            // -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
            else if (Row.ErrorColumn == -1)
            {
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables.";
            }
            else
            {
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);
            }
        }
    }
}
```

## <a name="see-also"></a>另請參閱  
 [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)   
 [在資料流程元件中使用錯誤輸出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
