---
title: 實作外部中繼資料 | Microsoft Docs
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
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 70e99073f07e7e285d1fcbfad51cf9a275dd9441
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387226"
---
# <a name="implementing-external-metadata"></a>實作外部中繼資料
  當元件從資料來源中斷連接時，可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100> 介面，針對其外部資料來源的資料行，驗證輸入及輸出資料行集合中的資料行。 這個介面可讓您維護在外部資料來源的資料行快照，並將這些資料行對應到元件的輸入和輸出資料行集合中的資料行。  
  
 實作外部中繼資料行會增加元件開發的負擔與複雜性，因為您必須維護和驗證其他的資料行集合，但是能夠避免因驗證而往返於伺服器的昂貴成本，因此這個開發工作仍是非常值得的。  
  
## <a name="populating-external-metadata-columns"></a>擴展外部中繼資料行  
 外部中繼資料行通常會在建立對應的輸入或輸出資料行時加入集合。 新資料行是透過呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A> 方法來建立。 接著會設定資料行的屬性以符合外部資料來源。  
  
 外部中繼資料行是透過將外部中繼資料行的識別碼指派到輸入或輸出資料行的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 屬性，以對應至相對應的輸入或輸入資料行。 這可讓您透過使用集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> 方法，輕易地找到特定輸入或輸出資料行的外部中繼資料行。  
  
 下列範例顯示如何建立外部中繼資料行，然後透過設定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 屬性將資料行對應至輸出資料行。  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>驗證外部中繼資料行  
 對於維護外部中繼資料行集合的元件，驗證將需要額外的步驟，因為您必須針對其他的資料行集合來驗證。 驗證可以分成連接式驗證或中斷連接式驗證。  
  
### <a name="connected-validation"></a>連接式驗證  
 當元件連接至外部資料來源時，會直接針對外部資料來源，驗證輸入或輸出集合中的資料行。 此外，也必須驗證外部中繼資料集合中的資料行。 這是必要的，因為透過使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中的 [進階編輯器] 即可修改外部中繼資料集合，而且對集合的變更是無法偵測的。 因此，在連接時，元件必須確定外部中繼資料資料行集合中的資料行會持續反映外部資料來源的資料行。  
  
 您可以選擇隱藏中的外部中繼資料集合**進階編輯器**藉由設定<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A>屬性的集合`false`。 然而這也可能會隱藏編輯器的 [資料行對應] 索引標籤，它可讓使用者從輸入或輸出集合將資料行對應到外部中繼資料行集合中的資料行。 將此屬性設定為 `false` 並不會防止開發人員以程式設計方式修改集合，但是確實可以為專用於 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 的元件之外部中繼資料行集合提供一層保護。  
  
### <a name="disconnected-validation"></a>中斷連接式驗證  
 當元件和外部資料來源中斷連接時，因為輸入或輸出集合中的資料行會直接針對外部中繼資料集合中的資料行 (而非針對外部來源) 進行驗證，驗證就較為簡單。 當元件連至其外部資料來源的連接尚未建立時，或是當 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性為 `false` 時，元件應該執行中斷連接式驗證。  
  
 下列程式碼範例示範元件的實作，以針對其外部中繼資料行集合執行驗證。  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../data-flow/data-flow.md)  
  
  
