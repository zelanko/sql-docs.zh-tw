---
title: 開發資料流程元件的使用者介面 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], custom editors
- user interfaces [Integration Services]
- custom data flow components [Integration Services], custom editors
- custom component editors [Integration Services]
- IDtsComponentUI interface
- UITypeName property
- custom user interface [Integration Services], custom data flow component
- editors [Integration Services]
ms.assetid: 10b829a1-609b-42e3-9070-cfe5a2bb698c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 21bc28f99768c7b31d6ba5b18170140a23400853
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287771"
---
# <a name="developing-a-user-interface-for-a-data-flow-component"></a>開發資料流程元件的使用者介面

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  元件開發人員可為元件提供自訂使用者介面，當編輯此元件時會在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中顯示此使用者介面。 實作自訂使用者介面會為您提供通知功能，讓您知道何時在資料流程工作中加入及刪除此元件，以及何時要求此元件的協助。  
  
 如果您並未針對元件提供自訂使用者介面，使用者仍然可以使用進階編輯器來設定此元件和它的自訂屬性。 您可以確保進階編輯器允許使用者適當地編輯自訂屬性值，其方式是在適當時使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 屬性。 如需詳細資訊，請參閱[資料流程元件的設計階段方法](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)中的＜建立自訂屬性＞。  
  
## <a name="setting-the-uitypename-property"></a>設定 UITypeName 屬性  
 若要提供自訂使用者介面，開發人員必須將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性設定為可實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 介面的類別名稱。 當此元件設定這個屬性時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中編輯此元件時載入及呼叫自訂使用者介面。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> 屬性是以逗號分隔的字串，可識別此類型的完整名稱。 下列清單將依序顯示可識別此類型的元素：  
  
-   類型名稱  
  
-   組件名稱  
  
-   檔案版本  
  
-   Culture  
  
-   公開金鑰 Token  
  
 下列程式碼範例顯示一個衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別的類別，並指定 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> 屬性。  
  
```csharp  
[DtsPipelineComponent(  
DisplayName="SampleComponent",  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...",  
ComponentType = ComponentType.Transform)]  
public class SampleComponent : PipelineComponent  
{  
//TODO: Implement the component here.  
}  
```  
  
```vb  
<DtsPipelineComponent(DisplayName="SampleComponent", _  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...", ComponentType=ComponentType.Transform)> _   
Public Class SampleComponent   
 Inherits PipelineComponent   
End Class  
```  
  
## <a name="implementing-the-idtscomponentui-interface"></a>實作 IDtsComponentUI 介面  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 介面包含了 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師在加入、刪除及編輯元件時所呼叫的方法。 元件開發人員可以在這些方法的實作中提供程式碼，以便與此元件的使用者互動。  
  
 此類別通常會在與元件本身不同的組件內實作。 雖然不需要使用不同的組件，但是這樣會讓開發人員彼此單獨來建立及部署元件和使用者介面，並讓元件的二進位檔維持在很小的使用量。  
  
 實作自訂使用者介面可讓元件開發人員對於此元件有更大的控制權，因為它是在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中編輯。 例如，元件可在 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> 方法中加入程式碼 (最初在資料流程工作中加入元件時會呼叫此方法)，並顯示一個精靈，引導使用者進行元件的初始組態設定。  
  
 當您建立一個可實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 介面的類別之後，您必須加入程式碼，以回應使用者與此元件的互動。 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 方法會提供此元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面，而且會在 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 方法之前呼叫。 這個參考應該儲存在私用成員變數中，而且會在之後用來修改此元件的中繼資料。  
  
## <a name="modifying-a-component-and-persisting-changes"></a>修改元件及保存變更  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面會當做參數提供給 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 方法。 這個參考應該由使用者介面程式碼快取在成員變數中，然後用來修改此元件，以回應使用者與使用者介面的互動。  
  
 雖然您可以透過 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面直接修改此元件，但是比較好的作法是使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> 方法建立 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> 執行個體。 當您使用此介面直接編輯元件時，您會略過此元件的驗證防護。 透過 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> 使用此元件之設計階段執行個體的優點如下：您可確保此元件可控制對它所做的變更。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 方法的傳回值會決定對元件所做的變更是會保存下來還是捨棄。 當這個方法傳回 **false** 時，所有的變更都會被捨棄；**true** 會保存對此元件所做的變更，並將此套件標示為需要儲存。  
  
### <a name="using-the-services-of-the-ssis-designer"></a>使用 SSIS 設計師的服務  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 方法的 **IServiceProvider** 參數會提供對下列 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工作服務的存取權：  
  
|服務|Description|  
|-------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsClipboardService>|用來判斷此元件是否在複製/貼上或剪下/貼上的作業中產生。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionService>|用來存取現有的連接或是在封裝中建立新的連接。|  
|<xref:Microsoft.SqlServer.Dts.Design.IErrorCollectionService>|當您需要擷取由此元件所引發的所有錯誤和警告，而不是只接收上一次的錯誤或警告時，用來從資料流程元件中擷取事件。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsVariableService>|用來存取現有的變數或是在封裝中建立新的變數。|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsPipelineEnvironmentService>|由資料流程元件用來存取父資料流程工作及資料流程中的其他元件。 這項功能可用來開發類似「緩時變維度精靈」的元件，該元件會視需要建立及連接其他資料流程元件。|  
  
 這些服務會提供元件開發人員能夠在此元件載入所在的封裝內存取及建立物件的功能。  
  
## <a name="sample"></a>範例  
 下列程式碼範例示範如何整合一個可實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 介面的自訂使用者介面類別，以及一個當做元件之編輯器的 Windows Form。  
  
### <a name="custom-user-interface-class"></a>自訂使用者介面類別  
 下列程式碼將示範實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 介面的類別。 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 方法會建立元件編輯器，然後顯示表單。 此表單的傳回值會決定是否保存對此元件所做的變更。  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline.Design;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public class SampleComponentUI : IDtsComponentUI  
    {  
        IDTSComponentMetaData100 md;  
        IServiceProvider sp;  
  
        public void Help(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void New(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void Delete(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Variables vars, Connections cons)  
        {  
            // Create and display the form for the user interface.  
            SampleComponentUIForm componentEditor = new SampleComponentUIForm(cons, vars, md);  
  
            DialogResult result  = componentEditor.ShowDialog(parentWindow);  
  
            if (result == DialogResult.OK)  
                return true;  
  
            return false;  
        }  
        public void Initialize(IDTSComponentMetaData100 dtsComponentMetadata, IServiceProvider serviceProvider)  
        {  
            // Store the component metadata.  
            this.md = dtsComponentMetadata;  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Windows.Forms   
Imports Microsoft.SqlServer.Dts.Runtime   
Imports Microsoft.SqlServer.Dts.Pipeline.Design   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Class SampleComponentUI   
 Implements IDtsComponentUI   
   Private md As IDTSComponentMetaData100   
   Private sp As IServiceProvider   
  
   Public Sub Help(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub New(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub Delete(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal vars As Variables, ByVal cons As Connections) As Boolean   
     ' Create and display the form for the user interface.  
     Dim componentEditor As SampleComponentUIForm = New SampleComponentUIForm(cons, vars, md)   
     Dim result As DialogResult = componentEditor.ShowDialog(parentWindow)   
     If result = DialogResult.OK Then   
       Return True   
     End If   
     Return False   
   End Function   
  
   Public Sub Initialize(ByVal dtsComponentMetadata As IDTSComponentMetaData100, ByVal serviceProvider As IServiceProvider)   
     Me.md = dtsComponentMetadata   
   End Sub   
 End Class   
  
End Namespace  
```  
  
### <a name="custom-editor"></a>自訂編輯器  
 下列程式碼示範在 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 方法的呼叫期間所顯示之 Windows Form 的實作。  
  
```csharp  
using System;  
using System.Drawing;  
using System.Collections;  
using System.ComponentModel;  
using System.Windows.Forms;  
using System.Data;  
  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public partial class SampleComponentUIForm : System.Windows.Forms.Form  
    {  
        private Connections connections;  
        private Variables variables;  
        private IDTSComponentMetaData100 metaData;  
        private CManagedComponentWrapper designTimeInstance;  
        private System.ComponentModel.IContainer components = null;  
  
        public SampleComponentUIForm( Connections cons, Variables vars, IDTSComponentMetaData100 md)  
        {  
            variables = vars;  
            connections = cons;  
            metaData = md;  
        }  
  
        private void btnOk_Click(object sender, System.EventArgs e)  
        {  
            if (designTimeInstance == null)  
                designTimeInstance = metaData.Instantiate();  
  
            designTimeInstance.SetComponentProperty( "CustomProperty", txtCustomPropertyValue.Text);  
  
            this.Close();  
        }  
  
        private void btnCancel_Click(object sender, System.EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Drawing   
Imports System.Collections   
Imports System.ComponentModel   
Imports System.Windows.Forms   
Imports System.Data   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Partial Class SampleComponentUIForm   
  Inherits System.Windows.Forms.Form   
   Private connections As Connections   
   Private variables As Variables   
   Private metaData As IDTSComponentMetaData100   
   Private designTimeInstance As CManagedComponentWrapper   
   Private components As System.ComponentModel.IContainer = Nothing   
  
   Public Sub New(ByVal cons As Connections, ByVal vars As Variables, ByVal md As IDTSComponentMetaData100)   
     variables = vars   
     connections = cons   
     metaData = md   
   End Sub   
  
   Private Sub btnOk_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     If designTimeInstance Is Nothing Then   
       designTimeInstance = metaData.Instantiate   
     End If   
     designTimeInstance.SetComponentProperty("CustomProperty", txtCustomPropertyValue.Text)   
     Me.Close   
   End Sub   
  
   Private Sub btnCancel_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     Me.Close   
   End Sub   
 End Class   
  
End Namespace  
```
  
## <a name="see-also"></a>另請參閱  
 [建立自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
  
  
