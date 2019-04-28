---
title: 建立和改變物件 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702295"
---
# <a name="creating-and-altering-objects-xmla"></a>建立和改變物件 (XMLA)
  主要物件可以獨立建立、改變和刪除。 主要物件包括下列物件：  
  
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
  
 您使用[Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)命令來建立執行個體上的主要物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，而[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令來改變執行個體上的現有主要物件。 這兩個命令會使用執行[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法。  
  
## <a name="creating-objects"></a>建立物件  
 當您使用 `Create` 方法建立物件時，必須先識別包含要建立的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件之父物件。 您藉由提供物件參考中的識別父物件[ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性`Create`命令。 每個物件參考都包含唯一識別 `Create` 命令的父物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[定義和識別物件&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
 例如，您必須提供物件參考給 Cube，來為 Cube 建立新的量值群組。 在 `ParentObject` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)元素包含 Analysis Services 指令碼語言 (ASSL) 元素，定義要建立的主要物件。 如需有關 ASSL 的詳細資訊，請參閱 <<c0> [ 使用 Analysis Services 指令碼語言來開發&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。</c0>  
  
 如果您將 `AllowOverwrite` 命令的 `Create` 屬性設定為 True，可以覆寫具有指定識別碼的現有主要物件。 否則，如果具有指定識別碼的主要物件已經在父物件中，就會發生錯誤。  
  
 如需詳細資訊`Create`命令，請參閱[建立的項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)。  
  
### <a name="creating-session-objects"></a>建立工作階段物件  
 工作階段物件是只能用於用戶端應用程式所使用的明確或隱含工作階段的暫存物件，而且會在結束工作階段時刪除。 您可以設定來建立工作階段物件`Scope`的屬性`Create`命令以*工作階段*。  
  
> [!NOTE]  
>  使用時*工作階段*設定，請`ObjectDefinition`元素只能包含[維度](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)， [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)，或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL項目。  
  
## <a name="altering-objects"></a>改變物件  
 藉由修改物件時`Alter`方法中，您必須先識別要修改提供中的物件參考的物件[物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性`Alter`命令。 每個物件參考都包含唯一識別 `Alter` 命令的物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[定義和識別物件&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
 例如，您必須提供物件參考給 Cube，以修改 Cube 的結構。 在 `Object` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 `ObjectDefinition` 元素包含定義要修改的主要物件之 ASSL 元素。 如需有關 ASSL 的詳細資訊，請參閱 <<c0> [ 使用 Analysis Services 指令碼語言來開發&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。</c0>  
  
 如果您將 `AllowCreate` 命令的 `Alter` 屬性設定為 True，只要物件不存在，即可建立指定的主要物件。 否則，如果指定的主要物件尚未存在，就會發生錯誤。  
  
### <a name="using-the-objectexpansion-attribute"></a>使用 ObjectExpansion 屬性  
 如果您要變更主要物件的屬性，而且未重新定義主要物件所含的次要物件，您可以設定`ObjectExpansion`的屬性`Alter`命令以*ObjectProperties*。 `ObjectDefinition` 屬性就只需要包含主要物件之屬性的元素，而且 `Alter` 命令不會改變與主要物件關聯的次要物件。  
  
 若要重新定義次要物件的主要物件，您必須設定`ObjectExpansion`屬性設定為*ExpandFull*和物件定義必須包含所有主要物件所含的次要物件。 如果 `ObjectDefinition` 命令的 `Alter` 屬性未明確包括主要物件所含的次要物件，則會刪除未包括的次要物件。  
  
### <a name="altering-session-objects"></a>改變工作階段物件  
 若要修改所建立的工作階段物件`Create`命令，將`Scope`屬性`Alter`命令*工作階段*。  
  
> [!NOTE]  
>  使用時*工作階段*設定，請`ObjectDefinition`元素只能包含[維度](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)， [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)，或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL項目。  
  
## <a name="creating-or-altering-subordinate-objects"></a>建立或改變從屬物件  
 雖然 `Create` 或 `Alter` 命令只會建立或修改一個最主要的物件，所建立或修改的主要物件，在其他主要物件或是其從屬的次要物件之封閉式 `ObjectDefinition` 屬性中，仍可包含定義。 例如，如果您定義一個 Cube，在 `ParentObject` 中指定父資料庫，並且在 `ObjectDefinition` 的 Cube 定義中，可以為 Cube 定義量值群組，而且在量值群組中，可以為每個量值群組，定義資料分割。 次要物件只能在包含它的主要物件之下定義。 如需有關主要和次要物件的詳細資訊，請參閱[資料庫物件&#40;Analysis Services-多維度資料&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會建立參考之關聯式資料來源[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
### <a name="code"></a>程式碼  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 `ObjectExpansion`的屬性`Alter`命令已設為*ObjectProperties*。 此設定可讓[ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)項目、 次要物件，從資料來源中定義要排除`ObjectDefinition`。 因此，資料來源的模擬資訊仍然會設定成服務帳號，如第一個範例中所指定。  
  
## <a name="see-also"></a>另請參閱  
 [Execute 方法&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
