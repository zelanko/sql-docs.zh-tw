---
title: Data Flow 可以使用運算式設定屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0dccc1a7bb932ae044f6d1e2491c7521652e9033
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146783"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>可以使用運算式設定的資料流程屬性
  可使用「資料流程」工作容器上提供的屬性運算式，以指定資料流程物件的某些屬性值。  
  
 如需使用屬性運算式的資訊，請參閱 [在封裝中使用屬性運算式](expressions/use-property-expressions-in-packages.md)。  
  
 您可以使用屬性運算式來為封裝之每個部署的執行個體自訂組態。 您也可以使用屬性運算式來指定封裝的執行階段條件約束，其方法是搭配 **dtexec** 命令提示字元公用程式使用 **/set** 選項。 例如，您可以限制`MaximumThreads`使用 「 排序 」 轉換，或`MaxMemoryUsage`「 模糊群組 」 和 「 模糊查閱 」 轉換。 如果未受到約束，這些轉換可能會在記憶體中快取大量的資料。  
  
 若要針對本主題所列的其中一個資料流程物件屬性指定屬性運算式，請顯示資料流程工作的 [屬性] 視窗，其方式是在設計工具的 [控制流程] 介面上選取資料流程工作，或是選取設計工具的 [資料流程] 索引標籤，而不需選取任何個別的元件或路徑。 選取 [運算式] 屬性，然後按一下省略符號 (...)，顯示 [屬性運算式編輯器] 對話方塊。 下拉 [屬性] 清單來選取屬性，然後在 [運算式] 文字方塊中輸入運算式，或是按一下省略符號 (...) 以顯示 [運算式產生器] 對話方塊。  
  
 [屬性] 清單只會針對您已經放在設計工具之 [資料流程] 介面上的那些資料流程物件來顯示可用的屬性。 因此，您無法使用 [屬性] 清單來檢視支援屬性運算式之資料流程物件的所有可能屬性。 例如，如果您在設計工具介面上放置 ADO NET 來源**屬性**清單包含的項目`[ADO NET Source].[SqlCommand]`屬性。 此清單也會顯示資料流程工作本身的許多屬性。  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>支援屬性運算式之資料流程物件的屬性  
 可以使用屬性運算式來指定下列清單中的屬性值。  
  
### <a name="data-flow-sources"></a>資料流程來源  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|ADO NET 來源|TableOrViewName 屬性<br /><br /> SqlCommand 屬性|  
|XML 來源|XMLData 屬性<br /><br /> XMLSchemaDefinition 屬性|  
  
### <a name="data-flow-transformations"></a>資料流程轉換  
 如需這些自訂屬性的詳細資訊，請參閱 [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)。  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|條件式分割轉換|FriendlyExpression 屬性|  
|衍生的資料行轉換|FriendlyExpression 屬性|  
|模糊群組轉換|MaxMemoryUsage 屬性|  
|模糊查閱轉換|MaxMemoryUsage 屬性|  
|查閱轉換|SqlCommand 屬性<br /><br /> SqlCommandParam 屬性|  
|OLE DB 命令轉換|SqlCommand 屬性|  
|百分比取樣轉換|SamplingValue 屬性|  
|樞紐轉換|PivotKeyValue 屬性|  
|資料列取樣轉換|SamplingValue 屬性|  
|排序轉換|MaximumThreads 屬性|  
|取消樞紐轉換|PivotKeyValue 屬性|  
  
### <a name="data-flow-destinations"></a>資料流程目的地  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|ADO NET 目的地|TableOrViewName 屬性<br /><br /> BatchSize 屬性<br /><br /> CommandTimeout 屬性|  
|一般檔案目的地|Header 屬性|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 目的地|TableName 屬性|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目的地|BulkInsertTableName 屬性<br /><br /> BulkInsertFirstRow 屬性<br /><br /> BulkInsertLastRow 屬性<br /><br /> BulkInsertOrder 屬性<br /><br /> Timeout 屬性|  
  
## <a name="related-tasks"></a>相關工作  
  
-   [新增或變更屬性運算式](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](http://pragmaticworks.com/cheatsheet/)  
  
## <a name="see-also"></a>另請參閱  
 [在封裝中使用屬性運算式](expressions/use-property-expressions-in-packages.md)   
 [通用屬性](../../2014/integration-services/common-properties.md)   
 [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)   
 [路徑屬性](../../2014/integration-services/path-properties.md)  
  
  