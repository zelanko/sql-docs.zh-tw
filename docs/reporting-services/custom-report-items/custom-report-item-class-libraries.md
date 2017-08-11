---
title: "自訂報表項目類別庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f216228c01e835e88cd9d4c7d7d4190648a386db
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="custom-report-item-class-libraries"></a>自訂報表項目類別庫
  自訂報表項目使用中的類別**m**命名空間。 用於實作自訂報表項目的類別可以分成兩個主要類別：設計為支援自訂報表項目基礎結構的唯一類別，以及封裝相關報表定義語言 (RDL) 元素之功能的 Managed 包裝函數類別。 如需如何使用這些類別的程式碼範例，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="custom-report-item-infrastructure-classes"></a>自訂報表項目基礎結構類別  
 下列類別可用於實作自訂報表項目。  
  
> [!NOTE]  
>  下表並非完整的清單，其中僅包含每個類別最常用的屬性和方法。  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 這是主要的自訂報表項目類別。 自訂報表項目實作的主要類別必須繼承自這個類別。  
  
#### <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|**名稱**|自訂報表項目的名稱。|  
|**型別**|自訂報表項目的類型。|  
|**CustomData**|<xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 物件，用來封裝在設計階段所指定的自訂報表項目資料屬性。|  
|**CustomProperties**|自訂報表項目的自訂屬性集合。|  
|**高度**|自訂報表項目控制項的高度。|  
|**寬度**|自訂報表項目控制項的寬度。|  
|**報表**|報表層級屬性的容器，例如報表中資料集的清單。|  
|**AltReportItem**|替代報表項目物件，用於不支援自訂報表項目執行階段控制項之處。|  
|**樣式**|自訂報表項目的樣式屬性。|  
|**裝飾**|用於控制項互動式編輯的裝飾視窗。|  
|**站台**|**ISite**的元件。|  
|**DesignerVerbCollection**|控制項捷徑功能表的自訂動詞命令陣列。|  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**BeginEdit**|啟動控制項的互動式編輯。|  
|**DoDefaultAction**|在回應按兩下控制項或在控制項上按 Return 鍵時呼叫。|  
|**EndEdit**|停用控制項的互動式編輯。|  
|**GetService**|傳回表示服務的物件。|  
|**InitializeNewComponent**|在建立新的自訂報表項目時呼叫。|  
|**失效**|重新繪製控制項的整個介面。|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|在物件拖曳到控制項上時呼叫。|  
|**OnPaint**|呼叫以回應**小畫家**事件。|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 這是用於識別自訂報表項目類型的屬性。 名稱必須符合的值\<**名稱**> 屬性**ReportItem**報表設計師組態檔中的項目。  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|建構 CustomReportItemAttribute 物件。|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 這是用於指定用於自訂報表項目設計師顯示名稱的屬性。  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|建構 LocalizedNameAttribute 物件。|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 **裝飾**類別可由自訂報表項目設計階段元件來設計介面主要矩形之外提供區域。 這些區域可以處理使用者介面事件，例如按一下滑鼠和拖放作業等。  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**OnShow**|時呼叫**裝飾**已啟動。|  
|**OnHide**|時呼叫**裝飾**停用。|  
|**小畫家**|呼叫以回應**小畫家**事件。|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|當拖曳物件時呼叫**裝飾**。|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 這個類別用來提供用來支援自訂報表項目顯示服務的集合**裝飾**自訂報表項目設計階段元件的物件。  
  
#### <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|**AdornerWindowBounds**|裝飾項視窗的界限。|  
|**AdornerWindowRegion**|裝飾項視窗的區域。|  
|**AdornerWindowGraphics**|裝飾項視窗的圖形內容。|  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|傳回翻譯成設計工具框架 (Frame) 座標的元件界限。|  
|**InvalidateAdorner**|停用裝飾項視窗。|  
|**PointToAdorner**|傳回翻譯成裝飾項視窗座標的點螢幕座標 (Screen Coordinate)。|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 這個類別可從自訂報表項目設計階段控制項用於叫用運算式編輯器。  
  
#### <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|**EditValue**|叫用運算式編輯器 (以給定的物件值初始化)。|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 這個類別是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 欄位的集合，可用於支援設計環境中的拖放事件。 繼承自**IReportItemDataObject**。  
  
#### <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|**DataSetName**|包含要卸除之欄位的資料集名稱。|  
|**欄位**|欄位的集合 (**Microsoft.ReportDesigner.Field**) 是要卸除。|  
  
## <a name="see-also"></a>另請參閱  
 [報表定義語言 &#40;SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [建立自訂報表項目執行階段元件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [建立自訂報表項目設計階段元件](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
