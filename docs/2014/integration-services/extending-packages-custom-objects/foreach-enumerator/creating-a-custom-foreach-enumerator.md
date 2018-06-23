---
title: 建立自訂 Foreach 列舉值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5c7cba14a14eca63e95abfb8da5a6784b7405bfa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133309"
---
# <a name="creating-a-custom-foreach-enumerator"></a>建立自訂 Foreach 列舉值
  建立自訂 Foreach 列舉值的步驟，與建立 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 之其他自訂物件的步驟類似：  
  
-   建立繼承自基底類別的新類別。 對於 Foreach 列舉值而言，基底類別是 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>。  
  
-   將可識別物件類型的屬性套用至類別。 對於 Foreach 列舉值而言，此屬性是 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>。  
  
-   覆寫基底類別之方法與屬性的實作。 對於 Foreach 列舉值而言，最重要的是 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。  
  
-   (選擇性) 開發自訂使用者介面。 對於 Foreach 列舉值而言，這需要實作 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI> 介面的類別。  
  
 自訂列舉值是由 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器所裝載。 在執行階段，<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器會呼叫自訂列舉值的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。 自訂列舉值會傳回可實作 `IEnumerable` 介面的物件，例如 `ArrayList`。 然後，<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 會逐一查看集合中的每一個元素、透過使用者定義的變數將目前元素的值提供給控制流程，然後在容器內執行此控制流程。  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>自訂 ForEach 列舉值使用者入門  
  
### <a name="creating-projects-and-classes"></a>建立專案和類別  
 因為所有的 Managed Foreach 列舉值都是從 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基底類別衍生，所以建立自訂 Foreach 列舉值的第一個步驟是以慣用的 Managed 程式語言建立類別庫專案，並建立繼承自此基底類別的類別。 在此衍生的類別中，您將覆寫基底類別的方法與屬性，以實作自訂功能。  
  
 在相同的方案中，為自訂使用者介面建立另一個類別庫專案。 建議您針對使用者介面使用不同的組件以便能輕鬆地部署，因為它允許您獨立地更新和重新部署 Foreach 列舉值或是其使用者介面。  
  
 透過使用強式名稱金鑰檔案，將兩個專案都設定成簽署將在建立時期產生的組件。  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>套用 DtsForEachEnumerator 屬性  
 將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 屬性套用至您已建立的類別，以便將它識別為Foreach 列舉值。 此屬性會提供設計階段資訊，例如 Foreach 列舉值的名稱和描述。 `Name`屬性會出現在可用的列舉值的下拉式清單上**集合** 索引標籤**Foreach 迴圈編輯器** 對話方塊。  
  
 使用 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> 屬性將 Foreach 列舉值連結至其自訂使用者介面。 如需取得此屬性所需的公開金鑰權杖，可以使用 **sn.exe -t**，從要用於簽署使用者介面組件的金鑰組 (.snk) 檔案顯示公開金鑰權杖。  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Namespace Microsoft.Samples.SqlServer.Dts  
    <DtsForEachEnumerator(DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")> _   
    Public Class MyEnumerator  
     Inherits ForEachEnumerator  
        'Insert code here.  
    End Class  
End Namespace  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsForEachEnumerator( DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")]  
    public class MyEnumerator : ForEachEnumerator  
    {  
        //Insert code here.  
    }  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-enumerator"></a>建立、部署和偵錯自訂列舉值  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中建立、部署和偵錯自訂 Foreach 列舉值的步驟，非常類似於其他類型的自訂物件所需的步驟。 如需詳細資訊，請參閱[建立、部署和偵錯自訂物件](../building-deploying-and-debugging-custom-objects.md)。  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多 with Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [撰寫自訂 Foreach 列舉值的程式碼](coding-a-custom-foreach-enumerator.md)   
 [開發自訂 Foreach 列舉程式的使用者介面](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  