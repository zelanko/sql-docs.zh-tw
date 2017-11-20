---
title: "建立自訂工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3d804ae69154913f4c5239a6bec304f14c4b856d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-task"></a>建立自訂工作
  建立自訂工作的步驟，與建立 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 之其他自訂物件的步驟類似：  
  
-   建立繼承自基底類別的新類別。 對於工作而言，基底類別是 <xref:Microsoft.SqlServer.Dts.Runtime.Task>。  
  
-   將可識別物件類型的屬性套用至類別。 對於工作而言，屬性是 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>。  
  
-   覆寫基底類別之方法與屬性的實作。 對於工作而言，這些包括 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法。  
  
-   (選擇性) 開發自訂使用者介面。 對於工作而言，這需要實作 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 介面的類別。  
  
## <a name="getting-started-with-a-custom-task"></a>自訂工作使用者入門  
  
### <a name="creating-projects-and-classes"></a>建立專案和類別  
 因為所有的 Managed 工作都是從 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基底類別衍生，所以建立自訂工作時的第一個步驟是以慣用的 Managed 程式語言建立類別庫專案，並建立從基底類別繼承的類別。 在此衍生的類別中，您將覆寫基底類別的方法與屬性，以實作自訂功能。  
  
 在相同的方案中，為自訂使用者介面建立另一個類別庫專案。 建議為使用者介面使用不同的組件以便能輕鬆地部署，因為它允許您獨立地更新和重新部署連接管理員或是其使用者介面。  
  
 透過使用強式名稱金鑰檔案，將兩個專案都設定成簽署將在建立時期產生的組件。  
  
### <a name="applying-the-dtstask-attribute"></a>套用 DtsTask 屬性  
 將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性套用至您已建立的類別，以便將它識別為工作。 此屬性提供如名稱、描述和工作類別等設計階段資訊。  
  
 使用 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> 屬性將工作連結至其自訂使用者介面。 若要取得的公開金鑰 token 所需的屬性，可以使用**sn.exe t**顯示從您想要用來簽署使用者介面組件的金鑰組 (.snk) 檔案的公開金鑰 token。  
  
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
  
## <a name="building-deploying-and-debugging-a-custom-task"></a>建置、部署和偵錯自訂工作  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中建立、部署和偵錯自訂工作的步驟，類似於其他類型的自訂物件所需的步驟。 如需詳細資訊，請參閱[Building，Deploying，and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [編寫自訂工作](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [自訂工作開發使用者介面](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  

