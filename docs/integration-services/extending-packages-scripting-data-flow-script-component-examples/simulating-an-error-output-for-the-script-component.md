---
title: 模擬指令碼元件的錯誤輸出 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], error output
- error outputs [Integration Services], Script component
ms.assetid: f8b6ecff-ac99-4231-a0e7-7ce4ad76bad0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 793e6070ab5ba5219f8a3c08470fb7850f844400
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770746"
---
# <a name="simulating-an-error-output-for-the-script-component"></a>模擬指令碼元件的錯誤輸出
  雖然您無法在指令碼元件中將輸出直接設定為錯誤輸出，以自動處理錯誤資料列，不過可以建立其他輸出並使用指令碼中的條件式邏輯，適時地將資料列導向此輸出，以重新產生內建錯誤輸出的功能。 您可能會想要加入兩個額外的輸出資料行，以接收發生錯誤的資料行之錯誤碼與識別碼，來模擬內建錯誤輸出的行為。  
  
 如果您需要加入對應至特定預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼之錯誤描述，可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法，這個方法可透過指令碼元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 屬性取得。  
  
## <a name="example"></a>範例  
 在此所示的範例使用設定成具有兩個同步輸出之轉換的指令碼元件。 指令碼元件的目的在於從 AdventureWorks 範例資料庫的地址資料中，篩選出錯誤資料列。 這個虛構的範例是假設，我們正在為北美的客戶準備促銷活動，並且需要篩選出不在北美的地址。  
  
#### <a name="to-configure-the-example"></a>若要設定範例  
  
1.  在建立新指令碼元件之前，建立連接管理員並設定資料流程來源，以便從 AdventureWorks 範例資料庫選取地址資料。 就這個只查看 CountryRegionName 資料行的範例而言，您可以直接使用 Person.vStateCountryProvinceRegion 檢視，或是聯結 Person.Address、Person.StateProvince 和 Person.CountryRegion 資料表以選取資料。  
  
2.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。 開啟**指令碼轉換編輯器**。  
  
3.  在 [指令碼] 頁面上，將 **ScriptLanguage** 屬性設定成您要用以撰寫指令碼的指令碼語言。  
  
4.  按一下 **[編輯指令碼]** 開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。  
  
5.  在 **Input0_ProcessInputRow** 方法中，鍵入或貼上下列範例程式碼。  
  
6.  關閉 VSTA。  
  
7.  在 [輸入資料行] 頁面上，選取您要在指令碼轉換中處理的資料行。 此範例只使用 CountryRegionName 資料行。 您保留未選取的可用輸入資料行，將會在資料流程中傳遞時保持不變。  
  
8.  在 [輸入及輸出] 頁面上，新增新的第二個輸出，並將其 **SynchronousInputID** 值設定為輸入的識別碼，這也是預設輸出的 **SynchronousInputID** 屬性值。 將兩個輸出的 **ExclusionGroup** 屬性設定為相同的非零值 (例如 1)，以指出將每個資料列導向僅兩個輸出的其中一個。 提供特殊的名稱給新錯誤輸出，例如 "MyErrorOutput"。  
  
9. 將額外輸出資料行加入新錯誤輸出，以擷取所需的錯誤資訊，這可能包含發生錯誤的資料行之錯誤碼與識別碼，以及或許還有錯誤描述。 此範例會建立新資料行 ErrorColumn 與 ErrorMessage。 如果您在自己的實作中擷取預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤，請確定加入錯誤號碼的 ErrorCode 資料行。  
  
10. 請記下指令碼元件將檢查錯誤條件之輸入資料行的識別碼值。 這個範例使用此資料行識別碼以擴展 ErrorColumn 值。  
  
11. 關閉**指令碼轉換編輯器**。  
  
12. 將指令碼元件的輸出附加至適當的目的地。 一般檔案目的地對於特定測試而言是最容易設定的。  
  
13. 執行封裝。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  If Row.CountryRegionName <> "Canada" _  
      And Row.CountryRegionName <> "United States" Then  
  
    Row.ErrorColumn = 68 ' ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America."  
    Row.DirectRowToMyErrorOutput()  
  
  Else  
  
    Row.DirectRowToOutput0()  
  
  End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
{  
  
  if (Row.CountryRegionName!="Canada"&&Row.CountryRegionName!="United States")  
  
  {  
    Row.ErrorColumn = 68; // ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America.";  
    Row.DirectRowToMyErrorOutput();  
  
  }  
  else  
  {  
  
    Row.DirectRowToOutput0();  
  
  }  
  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)   
 [在資料流程元件中使用錯誤輸出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
  
  
