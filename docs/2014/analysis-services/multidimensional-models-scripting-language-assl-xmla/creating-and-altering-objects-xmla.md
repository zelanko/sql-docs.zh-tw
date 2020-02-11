---
title: 建立和改變物件（XMLA） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
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
  
-   檢視方塊  
  
-   採礦模型  
  
-   角色  
  
-   與伺服器或資料庫相關聯的命令  
  
-   資料來源  
  
 您可以使用[create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)命令[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在的實例上建立主要物件，以及[alter 命令來改變實例](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)上現有的主要物件。 這兩個命令都是使用[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法來執行。  
  
## <a name="creating-objects"></a>建立物件  
 當您使用 `Create` 方法建立物件時，必須先識別包含要建立的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件之父物件。 您可以在`Create`命令的[ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性中提供物件參考，以識別父物件。 每個物件參考都包含唯一識別 `Create` 命令的父物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[&#40;XMLA&#41;定義和識別物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
 例如，您必須提供物件參考給 Cube，來為 Cube 建立新的量值群組。 在 `ParentObject` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)元素包含 Analysis Services 指令碼語言（ASSL）專案，這些元素會定義要建立的主要物件。 如需 ASSL 的詳細資訊，請參閱[使用 Analysis Services 指令碼語言進行開發 &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您將 `AllowOverwrite` 命令的 `Create` 屬性設定為 True，可以覆寫具有指定識別碼的現有主要物件。 否則，如果具有指定識別碼的主要物件已經在父物件中，就會發生錯誤。  
  
 如需`Create`命令的詳細資訊，請參閱[CREATE Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)。  
  
### <a name="creating-session-objects"></a>建立工作階段物件  
 工作階段物件是只能用於用戶端應用程式所使用的明確或隱含工作階段的暫存物件，而且會在結束工作階段時刪除。 您可以藉由將`Scope` `Create`命令的屬性設定為*session*來建立會話物件。  
  
> [!NOTE]  
>  使用*會話* `ObjectDefinition`設定時，元素只能包含[Dimension](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)、 [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 元素。  
  
## <a name="altering-objects"></a>改變物件  
 使用`Alter`方法修改物件時，您必須先在`Alter`命令的[object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性中提供物件參考，以識別要修改的物件。 每個物件參考都包含唯一識別 `Alter` 命令的物件所需的物件識別碼。 如需物件參考的詳細資訊，請參閱[&#40;XMLA&#41;定義和識別物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)。  
  
 例如，您必須提供物件參考給 Cube，以修改 Cube 的結構。 在 `Object` 屬性中的 Cube 之物件參考，包含資料庫識別碼與 Cube 識別碼，因為相同的 Cube 識別碼可能會用於不同的資料庫。  
  
 
  `ObjectDefinition` 元素包含定義要修改的主要物件之 ASSL 元素。 如需 ASSL 的詳細資訊，請參閱[使用 Analysis Services 指令碼語言進行開發 &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您將 `AllowCreate` 命令的 `Alter` 屬性設定為 True，只要物件不存在，即可建立指定的主要物件。 否則，如果指定的主要物件尚未存在，就會發生錯誤。  
  
### <a name="using-the-objectexpansion-attribute"></a>使用 ObjectExpansion 屬性  
 如果您只變更主要物件的屬性，而且不會重新定義主要物件所包含的次要物件，您可以將`ObjectExpansion` `Alter`命令的屬性設定為*ObjectProperties*。 
  `ObjectDefinition` 屬性就只需要包含主要物件之屬性的元素，而且 `Alter` 命令不會改變與主要物件關聯的次要物件。  
  
 若要重新定義主要物件的次要物件，您必須將`ObjectExpansion`屬性設定為*ExpandFull* ，而且物件定義必須包含主要物件所包含的所有次要物件。 如果 `ObjectDefinition` 命令的 `Alter` 屬性未明確包括主要物件所含的次要物件，則會刪除未包括的次要物件。  
  
### <a name="altering-session-objects"></a>改變工作階段物件  
 若要`Create`修改命令所建立的會話物件，請`Scope`將`Alter`命令的屬性設定為*session*。  
  
> [!NOTE]  
>  使用*會話* `ObjectDefinition`設定時，元素只能包含[Dimension](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)、 [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 元素。  
  
## <a name="creating-or-altering-subordinate-objects"></a>建立或改變從屬物件  
 雖然 `Create` 或 `Alter` 命令只會建立或修改一個最主要的物件，所建立或修改的主要物件，在其他主要物件或是其從屬的次要物件之封閉式 `ObjectDefinition` 屬性中，仍可包含定義。 例如，如果您定義一個 Cube，在 `ParentObject` 中指定父資料庫，並且在 `ObjectDefinition` 的 Cube 定義中，可以為 Cube 定義量值群組，而且在量值群組中，可以為每個量值群組，定義資料分割。 次要物件只能在包含它的主要物件之下定義。 如需主要和次要物件的詳細資訊，請參閱[資料庫物件 &#40;Analysis Services 多維度資料&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會建立參考[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫的關聯式資料來源。  
  
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
 `Alter`命令`ObjectExpansion`的屬性已設定為*ObjectProperties*。 此設定可讓[ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)元素（次要物件）從中`ObjectDefinition`定義的資料來源中排除。 因此，資料來源的模擬資訊仍然會設定成服務帳號，如第一個範例中所指定。  
  
## <a name="see-also"></a>另請參閱  
 [XMLA&#41;的 Execute 方法 &#40;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [使用 Analysis Services 指令碼語言進行開發 &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
