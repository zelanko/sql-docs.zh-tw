---
title: 建立自訂報表項目設計階段元件 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a9789c2d017200650bcae7b5f864da708e5c7453
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63194292"
---
# <a name="creating-a-custom-report-item-design-time-component"></a>建立自訂報表項目設計階段元件
  自訂報表項目設計階段元件是可用於 Visual Studio 報表設計工具環境的控制項。 自訂報表項目設計階段元件提供啟動的設計介面，這個介面與 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 屬性瀏覽器相整合，可接受拖放作業，並能夠提供自訂屬性編輯器。  
  
 藉由自訂報表項目設計階段元件，使用者可以在設計環境中將自訂報表項目放置於報表上，並在自訂報表項目上設定自訂屬性，然後再將自訂報表項目儲存為報表專案的一部分。  
  
 在程式開發環境中使用設計階段元件所設定的屬性，會由主設計環境序列化和還原序列化，然後儲存為報表定義語言 (RDL) 檔案中的元素。 當報表由報表處理器執行時，使用設計階段元件所設定的屬性會由報表處理器傳遞至自訂報表項目執行階段元件，這個元件會轉譯自訂報表項目，然後將其傳回給報表處理器。  
  
> [!NOTE]
>  自訂報表項目設計階段元件會實作為 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 元件。 本文件將描述自訂報表項目設計階段元件特定的實作詳細資料。 如需使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 來開發元件的詳細資訊，請參閱 MSDN Library 中的 [Visual Studio 中的元件](https://go.microsoft.com/fwlink/?LinkId=116576)。  
  
 如需完全實作的自訂報表項目的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="implementing-a-design-time-component"></a>實作設計階段元件  
 自訂報表項目設計階段元件的主類別是繼承自 **Microsoft.ReportDesigner.CustomReportItemDesigner** 類別。 除了用於 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 控制項的標準屬性外，元件類別還應該定義 **CustomReportItem** 屬性。 這個屬性必須與定義於 reportserver.config 檔案中的自訂報表項目的名稱相對應。 如需 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 屬性的清單，請參閱 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件集中的＜屬性＞。  
  
 下列程式碼範例示範套用至自訂報表項目設計階段控制項的屬性：  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>初始化元件  
 使用 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 類別傳遞自訂報表項目的使用者指定屬性。 您的 **CustomReportItemDesigner** 類別實作應該覆寫 **InitializeNewComponent** 方法，以建立元件 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 類別的新執行個體，並將其設定為預設值。  
  
 下列程式碼範例示範自訂報表項目設計階段元件類別，這個類別會覆寫 **CustomReportItemDesigner.InitializeNewComponent** 方法以初始化元件的 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 類別：  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>修改元件屬性  
 您可以用數種方式在設計環境中修改 **CustomData** 屬性。 您可以修改任何由設計階段元件所公開的屬性 (Property)，這些屬性都會藉由 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 屬性瀏覽器以 <xref:System.ComponentModel.BrowsableAttribute> 屬性 (Attribute) 標示。 此外，您也可以藉由下列方式修改屬性：將項目拖曳到自訂報表項目的設計介面，或者在設計環境中以滑鼠右鍵按一下控制項，然後選取捷徑功能表的 [屬性]  以顯示自訂屬性視窗。  
  
 下列程式碼範例示範套用 <xref:System.ComponentModel.BrowsableAttribute> 屬性的 **Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData** 屬性：  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 您可以使用自訂屬性編輯器對話方塊來提供設計階段元件。 自訂屬性編輯器實作應該繼承自 <xref:System.ComponentModel.ComponentEditor> 類別，而且會建立可用於屬性編輯的對話方塊執行個體。  
  
 下列範例示範繼承自 <xref:System.ComponentModel.ComponentEditor> 之類別的實作，並顯示自訂屬性編輯器對話方塊。  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 您的自訂屬性編輯器對話方塊可以叫用報表設計工具運算式編輯器。 在下列範例中，當使用者選取下拉式方塊中的第一個元素時就會叫用運算式編輯器。  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>使用設計工具動詞  
 設計工具動詞命令是連結至事件處理常式的功能表命令。 若要在設計環境中使用自訂報表項目執行階段控制項，您可以加入要顯示在元件之捷徑功能表的設計工具動詞命令。 您可以使用 **Verbs** 屬性，從執行階段元件傳回可用的設計工具動詞清單。  
  
 下列程式碼範例示範加入至 <xref:System.ComponentModel.Design.DesignerVerbCollection> 的設計工具動詞和事件處理常式，以及事件處理常式程式碼：  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>使用裝飾  
 自訂報表項目類別也可以實作 **Microsoft.ReportDesigner.Design.Adornment** 類別。 透過裝飾，自訂報表項目控制項可以在設計介面的主要矩形之外提供區域。 這些區域可以處理使用者介面事件，例如按一下滑鼠和拖放作業等。 定義於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Microsoft.ReportDesigner** 命名空間中的 **Adornment** 類別，是 Windows Forms 中 <xref:System.Windows.Forms.Design.Behavior.Adorner> 類別的傳遞實作。 如需 **Adorner** 類別的完整文件集，請參閱 MSDN Library 中的[行為服務概觀](https://go.microsoft.com/fwlink/?LinkId=116673)。 如需實作 **Microsoft.ReportDesigner.Design.Adornment** 類別的範例程式碼，請參閱 [SQL Server Reporting Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
 如需有關在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中進行程式開發和使用 Windows Form 的詳細資訊，請參閱 MSDN Library 中的下列主題：  
  
-   元件的設計階段屬性  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的元件  
  
-   逐步解說：建立利用 Visual Studio 設計階段功能的 Windows Forms 控制項  
  
## <a name="see-also"></a>另請參閱  
 [自訂報表項目架構](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [建立自訂報表項目執行階段元件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [自訂報表項目類別庫](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [操作說明：部署自訂報表項目](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
