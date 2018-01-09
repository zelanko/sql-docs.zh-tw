---
title: "建立和改變物件 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6906c6dbab99923983cbfa4e75c35c6f3c0f5073
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="creating-and-altering-objects-xmla"></a>建立和改變物件 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]主要物件可以是獨立建立、 改變和刪除。 主要物件包括下列物件：  
  
-   伺服器  
  
-   資料庫  
  
-   維度  
  
-   Cube  
  
-   量值群組  
  
-   資料分割  
  
-   「檢視方塊」  
  
-   採礦模型  
  
-   角色  
  
-   與伺服器或資料庫相關聯的命令  
  
-   資料來源  
  
 您使用[建立](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)命令的執行個體上建立主要物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，而[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令來改變執行個體上的現有主要物件。 這兩個命令會使用執行[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="creating-objects"></a>建立物件  
 當您建立的物件使用**建立**方法，您必須先識別父物件，其中包含[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]来建立物件。 您透過提供物件參考中的識別父物件[ParentObject](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)屬性**建立**命令。 每個物件參考都包含唯一識別的父物件所需的物件識別碼**建立**命令。 如需物件參考的詳細資訊，請參閱[定義和識別物件 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 例如，您必須提供物件參考給 Cube，來為 Cube 建立新的量值群組。 Cube 中的物件參考**ParentObject**屬性包含的資料庫識別碼和 cube 識別碼，因為相同的 cube 識別碼可能用不同的資料庫。  
  
 [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)元素包含定義要建立的主要物件的 Analysis Services 指令碼語言 (ASSL) 元素。 如需有關 ASSL 的詳細資訊，請參閱[開發使用 Analysis Services 指令碼語言 &#40;ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 如果您設定**AllowOverwrite**屬性**建立**命令為 true 時，您可以覆寫具有指定的識別碼的現有主要物件。 否則，如果具有指定識別碼的主要物件已經在父物件中，就會發生錯誤。  
  
 如需有關**建立**命令，請參閱[建立元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md).  
  
### <a name="creating-session-objects"></a>建立工作階段物件  
 工作階段物件是只能用於用戶端應用程式所使用的明確或隱含工作階段的暫存物件，而且會在結束工作階段時刪除。 您可以設定來建立工作階段物件**範圍**屬性**建立**命令*工作階段*。  
  
> [!NOTE]  
>  當使用*工作階段*設定， **ObjectDefinition**元素只能包含[維度](../../analysis-services/scripting/objects/dimension-element-assl.md)， [Cube](../../analysis-services/scripting/objects/cube-element-assl.md)，或[MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 元素。  
  
## <a name="altering-objects"></a>改變物件  
 使用修改的物件時**Alter**方法，您必須先識別要修改提供中的物件參考的物件[物件](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)屬性**Alter**命令。 每個物件參考都包含唯一識別的物件所需的物件識別碼**Alter**命令。 如需物件參考的詳細資訊，請參閱[定義和識別物件 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 例如，您必須提供物件參考給 Cube，以修改 Cube 的結構。 Cube 中的物件參考**物件**屬性包含的資料庫識別碼和 cube 識別碼，因為相同的 cube 識別碼可能用不同的資料庫。  
  
 **ObjectDefinition**元素包含定義要修改的主要物件的 ASSL 元素。 如需有關 ASSL 的詳細資訊，請參閱[開發使用 Analysis Services 指令碼語言 &#40;ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 如果您設定**AllowCreate**屬性**Alter**命令為 true，如果物件不存在，您可以建立指定的主要物件。 否則，如果指定的主要物件尚未存在，就會發生錯誤。  
  
### <a name="using-the-objectexpansion-attribute"></a>使用 ObjectExpansion 屬性  
 如果您要變更主要物件的屬性，而且未重新定義主要物件所含的次要物件，您可以設定**ObjectExpansion**屬性**Alter**命令*ObjectProperties*。 **ObjectDefinition**屬性就只需要包含的元素內容的主要物件，而**Alter**命令會保留不變的主要物件相關聯的次要物件。  
  
 若要重新定義次要物件的主要物件，您必須設定**ObjectExpansion**屬性*ExpandFull*和物件定義必須包含所有主要物件所含的次要物件。 如果**ObjectDefinition**屬性**Alter**命令未明確包括主要物件所包含的次要物件，卻沒有包含次要物件，會刪除。  
  
### <a name="altering-session-objects"></a>改變工作階段物件  
 若要修改所建立的工作階段物件**建立**命令，將**範圍**屬性**Alter**命令*工作階段*。  
  
> [!NOTE]  
>  當使用*工作階段*設定， **ObjectDefinition**元素只能包含[維度](../../analysis-services/scripting/objects/dimension-element-assl.md)， [Cube](../../analysis-services/scripting/objects/cube-element-assl.md)，或[MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 元素。  
  
## <a name="creating-or-altering-subordinate-objects"></a>建立或改變從屬物件  
 雖然**建立**或**Alter**命令建立或改變只能有一個最主要的物件時，正在建立或修改的主要物件可以包含在封入的定義**ObjectDefinition**其從屬的其他主要和次要物件的屬性。 比方說，如果您定義 cube 時，您指定的父資料庫**ParentObject**，以及在中的 cube 定義內**ObjectDefinition**您可以定義 cube 和量值中的量值群組您可以定義每個量值群組的資料分割的群組。 次要物件只能在包含它的主要物件之下定義。 如需有關主要和次要物件的詳細資訊，請參閱[資料庫物件 &#40;Analysis Services-多維度資料 &#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會建立關聯式資料來源參考[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
### <a name="code"></a>程式碼  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>描述  
 下列範例修改前面範例中所建立的關聯式資料來源，以便將資料來源的查詢逾時設定成 30 秒。  
  
### <a name="code"></a>程式碼  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>註解  
 **ObjectExpansion**屬性**Alter**命令已設為*ObjectProperties*。 此設定可讓[ImpersonationInfo](../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)元素、 次要物件，從資料來源中定義要排除**ObjectDefinition**。 因此，資料來源的模擬資訊仍然會設定成服務帳號，如第一個範例中所指定。  
  
## <a name="see-also"></a>請參閱  
 [執行方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [開發使用 Analysis Services 指令碼語言 &#40;ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
