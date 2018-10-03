---
title: DISCOVER_CSDL_METADATA 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: a2d3cffd-a2c4-411c-b244-9e41ebe30939
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27e3a36850dcf0d314398e994485d5e7410f9a8a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051388"
---
# <a name="discovercsdlmetadata-rowset"></a>DISCOVER_CSDL_METADATA 資料列集
  傳回有關 (表格式或多維度) [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料模型的資訊，提供 CSDLBI (概念結構定義語言商業智慧註解) 格式的模型定義。 CSDLBI 是以 CSDL 為基礎，它是實體資料架構所使用的 XML 結構描述，用於 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器與 [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] 用戶端之間的通訊。 商業智慧 (BI) 註解提供了有關表格式模型和其中所含物件的其他中繼資料。 如需表格式資料模型的詳細資訊，請參閱[商業智慧的 CSDL 註解 &#40;CSDLBI&#41;](../../tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
 命令的安全性內容會影響傳回的資料列集。 若要從伺服器取得 CSDL 定義，需要 Analysis Services 執行個體的讀取權限。  
  
 發出資料列集要求之用戶端的語言識別碼包含在命令的連接字串中，而且會影響傳回為資料列集一部分之數個屬性中顯示的語言。  如需有關可能受到語言識別碼影響之屬性和描述的詳細資訊，請參閱＜備註＞一節。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_CSDL_METADATA`資料列集包含下列資料行。  
  
|**資料行名稱**|**類型指標**|**限制**|**說明**|  
|---------------------|------------------------|---------------------|---------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|是|指定要求其 CSDLBI 描述之資料庫的名稱。 如果省略，就會使用目前的資料庫。<br /><br /> 這是所有模型類型的必要限制。|  
|`PERSPECTIVE_ID`|`DBTYPE_WSTR`|是|指定已在 CATALOG_NAME 指定的模型上定義之檢視方塊的識別碼。<br /><br /> 選擇性限制。 適用於所有模型類型。|  
|`PERSPECTIVE_NAME`|`DBTYPE_WSTR`|是|指定已在 CATALOG_NAME 指定的模型上定義之檢視方塊的名稱。<br /><br /> 這是表格式模型包含檢視方塊或多維度方案包含多個 Cube 或檢視方塊時的必要限制。|  
|`METADATA`|`DBTYPE_WSTR`|否|根據 CSDLBI 結構描述，包含資料來源及其屬性之 XML 定義的字串。|  
|`CUBE_ID`|`DBTYPE_WSTR`|是|字串識別碼。<br /><br /> 這是多維度資料庫的選擇性限制。 如果有多個可用的 Cube 且已省略限制，則會傳回預設 Cube。|  
  
## <a name="remarks"></a>備註  
 DISCOVER_CSDL_METADATA 具有下列需求：  
  
-   如果未使用 CATALOG_NAME 限制指定資料庫，DISCOVER 要求將會失敗。  
  
-   若是表格式模型，模型中有多個檢視方塊時就需要檢視方塊識別碼。  
  
-   若是多維度模型，目錄名稱和 Cube (檢視方塊) 名稱都是必要。  
  
-   如果檢視方塊當做限制提供，系統會針對模型傳回相同的 CSDL 資料列集。 不過，位於模型中但不包含在指定的檢視方塊中的任何物件會標示為 `Hidden` = True。  
  
-   對於資料表和資料行，DISCOVER 資料列集一律從 Cube 維度輸出值。 如果未設定 Cube 維度屬性，要求會從維度傳回值。  
  
-   DISCOVER 要求無法傳回包含語意錯誤的任何量值或導出資料行。  
  
-   對於沒有屬性值的物件，DISCOVER 要求將不會傳回任何資訊。 對於使用預設值的屬性，DISCOVER 要求也不會傳回任何值。  
  
 在資料列集中傳回的 XML 字串可能包含下列語言專屬的屬性或值。 例如，如果您從用戶端發出 LCID 為 0403 (卡達隆尼亞文西班牙文) 的資料列集要求，屬性將會傳回下列值 (如果適合卡達隆尼亞文西班牙文)。 如果伺服器上沒有翻譯，就會傳回伺服器預設語言的字串。  
  
-   Caption  
  
-   Qualifier  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 XMLA 查詢會傳回 AdventureWorks 2012 表格式模型範例的 CSDL 表示。 每個表格式方案只能包含一個模型，因此 PERSPECTIVE_NAME 限制可以保留空白。 不過，此模型包含多個檢視方塊。  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 XMLA 查詢會傳回 Contoso Operations Cube 的 CSDLBI 表示。 必須有 VERSION 限制才能查詢多維度資料庫。 Contoso Retail 資料庫包含兩個 Cube，因此 Operations Cube 是使用 PERSPECTIVE_NAME 限制參考。  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 結構描述資料列集](../analysis-services-schema-rowsets.md)   
 [商業智慧的 CSDL 註解&#40;CSDLBI&#41;](../../tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
