---
title: 建立和改變物件 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9702046c3e3c9e9ab0e9ff525d832baf611fe4b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023009"
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
  
 您使用[建立](../xmla/xml-elements-commands/create-element-xmla.md)命令的執行個體上建立主要物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，而[Alter](../xmla/xml-elements-commands/alter-element-xmla.md)命令來改變執行個體上的現有主要物件。 這兩個命令會使用執行[Execute](../xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="creating-objects"></a>建立物件  
 當您使用 `Create` 方法建立物件時，必須先識別包含要建立的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件之父物件。 您透過提供物件參考中的識別父物件[ParentObject](../xmla/xml-elements-properties/object-element-xmla.md)屬性`Create`命令。 每個物件參考都包含唯一識別 `Create` 命令的父物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[定義和識別物件&#40;XMLA&#41;](../xmla/xml-elements-objects.md)。  
  
 例如，您必須提供物件參考給 Cube，來為 Cube 建立新的量值群組。 在 `ParentObject` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 [ObjectDefinition](../xmla/xml-elements-properties/objectdefinition-element-xmla.md)元素包含定義要建立的主要物件的 Analysis Services 指令碼語言 (ASSL) 元素。 如需有關 ASSL 的詳細資訊，請參閱[使用 Analysis Services 指令碼語言來開發&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您將 `AllowOverwrite` 命令的 `Create` 屬性設定為 True，可以覆寫具有指定識別碼的現有主要物件。 否則，如果具有指定識別碼的主要物件已經在父物件中，就會發生錯誤。  
  
 如需有關`Create`命令，請參閱[建立項目&#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md)。  
  
### <a name="creating-session-objects"></a>建立工作階段物件  
 工作階段物件是只能用於用戶端應用程式所使用的明確或隱含工作階段的暫存物件，而且會在結束工作階段時刪除。 您可以設定來建立工作階段物件`Scope`屬性`Create`命令*工作階段*。  
  
> [!NOTE]  
>  當使用*工作階段*設定，`ObjectDefinition`元素只能包含[維度](../scripting/objects/dimension-element-assl.md)， [Cube](../scripting/objects/cube-element-assl.md)，或[MiningModel](../scripting/objects/miningmodel-element-assl.md) ASSL項目。  
  
## <a name="altering-objects"></a>改變物件  
 使用修改的物件時`Alter`方法，您必須先識別要修改提供中的物件參考的物件[物件](../xmla/xml-elements-properties/object-element-xmla.md)屬性`Alter`命令。 每個物件參考都包含唯一識別 `Alter` 命令的物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[定義和識別物件&#40;XMLA&#41;](../xmla/xml-elements-objects.md)。  
  
 例如，您必須提供物件參考給 Cube，以修改 Cube 的結構。 在 `Object` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 `ObjectDefinition` 元素包含定義要修改的主要物件之 ASSL 元素。 如需有關 ASSL 的詳細資訊，請參閱[使用 Analysis Services 指令碼語言來開發&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您將 `AllowCreate` 命令的 `Alter` 屬性設定為 True，只要物件不存在，即可建立指定的主要物件。 否則，如果指定的主要物件尚未存在，就會發生錯誤。  
  
### <a name="using-the-objectexpansion-attribute"></a>使用 ObjectExpansion 屬性  
 如果您要變更主要物件的屬性，而且未重新定義主要物件所含的次要物件，您可以設定`ObjectExpansion`屬性`Alter`命令*ObjectProperties*。 `ObjectDefinition` 屬性就只需要包含主要物件之屬性的元素，而且 `Alter` 命令不會改變與主要物件關聯的次要物件。  
  
 若要重新定義次要物件的主要物件，您必須設定`ObjectExpansion`屬性*ExpandFull*和物件定義必須包含所有主要物件所含的次要物件。 如果 `ObjectDefinition` 命令的 `Alter` 屬性未明確包括主要物件所含的次要物件，則會刪除未包括的次要物件。  
  
### <a name="altering-session-objects"></a>改變工作階段物件  
 若要修改所建立的工作階段物件`Create`命令，將`Scope`屬性`Alter`命令*工作階段*。  
  
> [!NOTE]  
>  當使用*工作階段*設定，`ObjectDefinition`元素只能包含[維度](../scripting/objects/dimension-element-assl.md)， [Cube](../scripting/objects/cube-element-assl.md)，或[MiningModel](../scripting/objects/miningmodel-element-assl.md) ASSL項目。  
  
## <a name="creating-or-altering-subordinate-objects"></a>建立或改變從屬物件  
 雖然 `Create` 或 `Alter` 命令只會建立或修改一個最主要的物件，所建立或修改的主要物件，在其他主要物件或是其從屬的次要物件之封閉式 `ObjectDefinition` 屬性中，仍可包含定義。 例如，如果您定義一個 Cube，在 `ParentObject` 中指定父資料庫，並且在 `ObjectDefinition` 的 Cube 定義中，可以為 Cube 定義量值群組，而且在量值群組中，可以為每個量值群組，定義資料分割。 次要物件只能在包含它的主要物件之下定義。 如需有關主要和次要物件的詳細資訊，請參閱[資料庫物件&#40;Analysis Services-多維度資料&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)。  
  
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
 `ObjectExpansion`屬性`Alter`命令已設為*ObjectProperties*。 此設定可讓[ImpersonationInfo](../scripting/properties/impersonationinfo-element-assl.md)元素、 次要物件，從資料來源中定義要排除`ObjectDefinition`。 因此，資料來源的模擬資訊仍然會設定成服務帳號，如第一個範例中所指定。  
  
## <a name="see-also"></a>另請參閱  
 [Execute 方法&#40;XMLA&#41;](../xmla/xml-elements-methods-execute.md)   
 [使用 Analysis Services 開發的指令碼語言&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  