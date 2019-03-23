---
title: 開發自訂工作的使用者介面 | Microsoft Docs
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
- custom user interfaces [Integration Services]
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- custom tasks [Integration Services], user interface
- custom user interface [Integration Services], custom tasks
- user interface [Integration Services]
- SSIS custom tasks, user interface
ms.assetid: 1e940cd1-c5f8-4527-b678-e89ba5dc398a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6268fe16c31c931dc71ad1a62bd72e08b1ecb537
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381786"
---
# <a name="developing-a-user-interface-for-a-custom-task"></a>開發自訂工作的使用者介面
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 物件模型會提供自訂工作開發人員能夠輕鬆地針對工作建立自訂使用者介面的能力 (該介面之後可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中整合及顯示)。 使用者介面可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中提供有用的資訊給使用者，然後指引使用者正確地設定自訂工作的屬性和設定。  
  
 為工作開發自訂使用者介面牽涉到兩個重要類別的使用。 下表將描述這些類別。  
  
|類別|描述|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|識別受管理的工作，並透過它的屬性來提供設計階段資訊，以控制 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師如何顯示物件以及與物件互動的屬性。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|此工作所使用，以便將此工作與其自訂使用者介面產生關聯的介面。|  
  
 本章節描述當您為自訂工作開發使用者介面時 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性和 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 介面的角色，並提供有關如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師內建立、整合、部署及偵錯此工作的詳細資料。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師針對此工作提供使用者介面的多個進入點：使用者可以在捷徑功能表上選取 [編輯]、按兩下此工作，或是按一下屬性表底部的 [顯示編輯器] 連結。 當使用者存取其中一個進入點時，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師就會尋找及載入包含此工作之使用者介面的組件。 此工作的使用者介面要負責建立對話方塊的屬性，該對話方塊會在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中顯示給使用者。  
  
 工作和它的使用者介面是不同的實體。 它們應該在不同的組件中實作，以減少當地語系化、部署和維護工作。 工作 DLL 不會載入、呼叫，或是通常會包含有關其使用者介面的任何知識，除了在工作中編碼之 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性值內包含的資訊以外。 這是工作與其使用者介面產生關聯的唯一方式。  
  
## <a name="the-dtstask-attribute"></a>DtsTask 屬性  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性會包含在工作類別程式碼中，好讓工作與其使用者介面產生關聯。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會使用此屬性 (Attribute) 的屬性 (Property) 來決定此工作如何顯示在設計師內。 這些屬性包含顯示名稱和圖示 (如果有的話)。  
  
 下表描述 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性 (Attribute) 的屬性 (Property)。  
  
|屬性|描述|  
|--------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>|在控制流程工具箱內顯示工作名稱。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>|工作描述 (繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute>)。 這個屬性會顯示在工具提示中。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A>|顯示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中的圖示。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.RequiredProductLevel%2A>|如果有使用的話，請將它設定為 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProductLevel> 列舉內的其中一個值。 例如， `RequiredProductLevel = DTSProductLevel.None` 。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskContact%2A>|保留連絡人資訊給此工作需要技術支援的情況使用。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskType%2A>|指派類型給此工作。|  
|Attribute.TypeId|在衍生類別中實作時，取得這個屬性的唯一識別碼。 如需詳細資訊，請參閱 .NET Framework 類別庫中的 `Attribute.TypeID` 屬性。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A>|此組件的類型名稱，由 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師用來載入此組件。 這個屬性是用來尋找此工作的使用者介面組件。|  
  
 下列程式碼範例會顯示 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 的面貌 (在類別定義上方編碼)。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會使用此屬性 (Attribute) 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> 屬性 (Property)，該屬性 (Attribute) 包含組件名稱、類型名稱、版本、文化特性和公開金鑰 Token，以便在全域組件快取 (GAC) 中尋找組件，並載入它供設計師使用。  
  
 當找到組件以後，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會使用此屬性 (Attribute) 中的其他屬性 (Property)，在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中顯示有關此工作的其他資訊，例如此工作的名稱、圖示和描述。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> 屬性會指定此工作要如何呈現給使用者。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> 屬性包含內嵌在使用者介面組件內之圖示的資源識別碼。 此設計師會從組件中依照識別碼載入圖示資源，並在此工作加入到封裝時，將它顯示在工具箱和設計介面上的工作名稱旁邊。 如果工作不提供圖示資源，設計師會針對此工作使用預設圖示。  
  
## <a name="the-idtstaskui-interface"></a>IDTSTaskUI 介面  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 介面會定義 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師所呼叫之方法和屬性的集合，以初始化及顯示與此工作有關的使用者介面。 當叫用工作的使用者介面時，設計師會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.Initialize%2A> 方法 (當您撰寫此方法時，它會由工作使用者介面所實作)，然後分別提供此工作和封裝的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 和 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合當做參數。 這些集合會儲存在本機，而且之後會在 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 方法中使用。  
  
 設計師會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 方法，要求顯示於 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中的視窗。 此工作會建立包含此工作之使用者介面的視窗執行個體，並將此使用者介面傳回給設計師以供顯示。 一般來說，<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 和 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 物件會透過多載建構函式提供給視窗，好讓它們可用於設定工作。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會呼叫工作使用者介面的 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 方法，以顯示此工作的使用者介面。 此工作使用者介面會從這個方法傳回 Windows Form，而 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會將這個表單顯示為強制回應對話方塊。 當關閉此表單時，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會檢查此表單之 `DialogResult` 屬性的值，以判斷此工作是否已經修改過，以及是否應該儲存這些修改。 如果 `DialogResult` 屬性的值是 `OK`，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會呼叫此工作的保存方法來儲存變更，否則會捨棄這些變更。  
  
 下列程式碼範例會實作 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 介面，並假設有一個名為 SampleTaskForm 的 Windows Form 類別存在。  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Design;  
  
namespace Sample  
{  
   public class HelloWorldTaskUI : IDtsTaskUI  
   {  
      TaskHost   taskHost;  
      Connections connections;  
      public void Initialize(TaskHost taskHost, IServiceProvider serviceProvider)  
      {  
         this.taskHost = taskHost;  
         IDtsConnectionService cs = serviceProvider.GetService  
         ( typeof( IDtsConnectionService ) ) as   IDtsConnectionService;   
         this.connections = cs.GetConnections();  
      }  
      public ContainerControl GetView()  
      {  
        return new HelloWorldTaskForm(this.taskHost, this.connections);  
      }  
     public void Delete(IWin32Window parentWindow)  
     {  
     }  
     public void New(IWin32Window parentWindow)  
     {  
     }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Design  
Imports System.Windows.Forms  
  
Public Class HelloWorldTaskUI  
  Implements IDtsTaskUI  
  
  Dim taskHost As TaskHost  
  Dim connections As Connections  
  
  Public Sub Initialize(ByVal taskHost As TaskHost, ByVal serviceProvider As IServiceProvider) _  
    Implements IDtsTaskUI.Initialize  
  
    Dim cs As IDtsConnectionService  
  
    Me.taskHost = taskHost  
    cs = DirectCast(serviceProvider.GetService(GetType(IDtsConnectionService)), IDtsConnectionService)  
    Me.connections = cs.GetConnections()  
  
  End Sub  
  
  Public Function GetView() As ContainerControl _  
    Implements IDtsTaskUI.GetView  
  
    Return New HelloWorldTaskForm(Me.taskHost, Me.connections)  
  
  End Function  
  
  Public Sub Delete(ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.Delete  
  
  End Sub  
  
  Public Sub [New](ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.[New]  
  
  End Sub  
  
End Class  
```  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作](creating-a-custom-task.md)   
 [撰寫自訂工作的程式碼](coding-a-custom-task.md)   
 [開發自訂工作的使用者介面](developing-a-user-interface-for-a-custom-task.md)  
  
  
