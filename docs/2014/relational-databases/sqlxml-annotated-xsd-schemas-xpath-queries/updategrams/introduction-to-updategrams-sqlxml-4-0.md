---
title: Updategram (SQLXML 4.0) 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 114bc96623b608cfbb520a9d2f35f23a04310a74
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014795"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Updategram 簡介 (SQLXML 4.0) 
  您可以修改 （插入、 更新或刪除） 中的資料庫[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]從現有的 XML 文件使用 updategram 或 OPENXML[!INCLUDE[tsql](../../../includes/tsql-md.md)]函式。  
  
 OPENXML 函數可透過切割現有的 XML 文件，並提供可以傳遞到 INSERT、UPDATE 或 DELETE 陳述式之資料列集來修改資料庫。 利用 OPENXML，可以針對資料庫資料表直接執行作業。 因此，每當資料列集提供者 (例如資料表) 可以當做來源顯示時，OPENXML 最適合。  
  
 Updategram 跟 OPENXML 一樣，可讓您在資料庫中插入、更新或刪除資料，不過，Updategram 會根據註解式 XSD (或 XDR) 結構描述提供的 XML 檢視運作，例如，更新會套用到對應結構描述提供的 XML 檢視。 對應結構描述會依序擁有將 XML 元素和屬性對應到對應的資料庫資料表和資料行的必要資訊。 Updategram 會使用此對應資訊來更新資料庫資料表和資料行。  
  
> [!NOTE]  
>  本文件集假設您非常熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的範本和對應結構描述支援。 如需詳細資訊，請參閱 <<c0> [ 註解式 XSD 結構描述簡介&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。</c0> 如需使用 XDR 的舊版應用程式，請參閱 < [Annotated XDR Schemas&#40;在 SQLXML 4.0 中已被取代&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="required-namespaces-in-the-updategram"></a>Updategram 中的必要命名空間  
 在 updategram 中，關鍵字這類**\<同步 >**， **\<之前 >**，以及**\<之後 >**，存在於`urn:schemas-microsoft-com:xml-updategram`命名空間。 您使用的命名空間前置詞是任意的。 在此文件集中，`updg` 前置詞代表 `updategram` 命名空間。  
  
## <a name="reviewing-syntax"></a>檢閱語法  
 Updategram 會使用範本**\<同步 >**， **\<之前 >**，以及**\<之後 >** 形成的語法的區塊updategram。 下列程式碼以其簡單的形式顯示此語法：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 下列定義描述每個區塊的角色：  
  
 **\<before>**  
 識別記錄執行個體的目前狀態 (也稱為「之前的狀態」)。  
  
 **\<after>**  
 識別所要變更資料的新狀態。  
  
 **\<sync>**  
 包含**\<之前 >** 並**\<之後 >** 區塊。 A **\<同步 >** 區塊可以包含多個一組**\<之前 >** 並**\<之後 >** 區塊。 如果有多個一組**\<之前 >** 並**\<之後 >** 區塊，這些區塊 （即使它們是空的） 必須指定為組。 此外，一個 updategram 可以有多個**\<同步 >** 區塊。 每個**\<同步 >** 區塊就是一個交易單位 (表示項目中**\<同步 >** 區塊完成，或執行任何動作)。 如果您指定多個**\<同步 >** 封鎖在 updategram 中，其中一個失敗**\<同步 >** 區塊不會影響其他**\<同步處理>** 區塊。  
  
 Updategram 是否刪除、 插入或更新記錄執行個體均視內容而定**\<之前 >** 並**\<之後 >** 區塊：  
  
-   如果記錄執行個體只會顯示在**\<之前 >** 區塊中沒有對應執行個體**\<之後 >** 區塊中，updategram 會執行刪除作業。  
  
-   如果記錄執行個體只會顯示在**\<之後 >** 區塊中沒有對應執行個體**\<之前 >** 區塊，它是一個插入作業。  
  
-   如果記錄執行個體出現在**\<之前 >** 封鎖，而且有對應的執行個體**\<之後 >** 區塊中，這是更新作業。 在此情況下，updategram 會更新記錄執行個體中所指定的值**\<之後 >** 區塊。  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>指定 Updategram 中的對應結構描述  
 在 Updategram 中，對應結構描述 (同時支援 XSD 和 XDR 結構描述) 提供的 XML 摘要可以是隱含的或明確的 (也就是說，Updategram 可以選擇是否搭配指定的對應結構描述使用)。 如果您未指定對應結構描述，updategram 會假設為隱含的對應 （預設對應），其中每個項目**\<之前 >** 區塊或**\<之後 >** 區塊會對應到資料表，而每個元素的子元素或屬性會對應到資料庫中的資料行。 如果您明確地指定對應結構描述，Updategram 中的元素和屬性必須符合對應結構描述中的元素和屬性。  
  
### <a name="implicit-default-mapping"></a>隱含的 (預設) 對應  
 在多數情況下，執行簡單更新的 Updategram 可能不需要對應結構描述。 在此情況下，Updategram 會依賴預設對應結構描述。  
  
 下列 Updategram 示範隱含的對應。 在這個範例中，Updategram 會在 Sales.Customer 資料表中插入新客戶。 此 updategram 使用隱含的對應，因為\<Sales.Customer > 元素會對應到 Sales.Customer 資料表，而 CustomerID 和 SalesPersonID 屬性會對應至 Sales.Customer 資料表中對應的資料行。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>明確的對應  
 如果您指定對應結構描述 (XSD 或 XDR)，Updategram 會使用結構描述來判斷要更新的資料庫資料表和資料行。  
  
 如果 Updategram 執行複雜的更新 (例如，根據在對應結構描述中指定的父子式關聯性，將記錄插入多個資料表)，您必須使用 Updategram 執行所依據的 `mapping-schema` 屬性，明確地提供對應結構描述。  
  
 由於 Updategram 是一個範本，因此，在 Updategram 中針對對應結構描述所指定的路徑是範本檔位置的相對路徑 (相對於儲存 Updategram 的位置)。 如需詳細資訊，請參閱 <<c0> [ 在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。</c0>  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Updategram 中的元素中心及屬性中心對應  
 利用預設對應 (在 Updategram 中未指定對應結構描述時)，Updategram 元素會對應到資料表，而子元素 (如果是元素中心對應) 和屬性 (如果是屬性中心對應) 則會對應到資料行。  
  
### <a name="element-centric-mapping"></a>元素中心的對應  
 在元素中心的 Updategram 中，一個元素包含表示元素屬性的多個子元素。 例如，請參閱下列 Updategram。  **\<Person.Contact >** 項目包含 **\<FirstName >** 並 **\<LastName >** 子項目。 這些子項目是屬性 **\<Person.Contact >** 項目。  
  
 這個 updategram 未指定對應結構描述，因此 updategram 會使用隱含的對應，其中 **\<Person.Contact >** 元素會對應到 Person.Contact 資料表，而其子項目對應到 FirstName 和LastName 資料行。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>以屬性為主的對應  
 在屬性中心的對應中，元素擁有屬性。 下列 Updategram 使用屬性中心的對應。 在此範例中，  **\<Person.Contact >** 元素所組成**FirstName**並**LastName**屬性。 這些屬性是屬性 **\<Person.Contact >** 項目。 如同上述範例中，這個 updategram 會指定任何對應結構描述中，因此它會依賴隱含的對應來對應 **\<Person.Contact >** Person.Contact 資料表，以及要將元素的屬性的項目資料表中的個別資料行。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>同時使用元素中心和屬性中心的對應  
 您可以指定混用的元素中心與屬性中心對應，如下列 Updategram 所示。 請注意，  **\<Person.Contact >** 項目包含屬性和子項目。 同時，這個 Updategram 依賴隱含的對應。 因此， **FirstName**屬性並 **\<LastName >** 子元素會對應到 Person.Contact 資料表中的對應資料行。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>使用在 SQL Server 有效，但在 XML 無效的字元  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，資料表名稱可以包含一個空格。 不過，此種類型的資料表名稱在 XML 中無效。  
  
 有效的字元編碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]識別碼，但是並非有效的 XML 識別碼，請使用 '__xHHHH\_\_' 當做編碼值，其中 HHHH 代表在大部分字元四位數字十六進位 ucs-2 代碼重要的位元第一順序。 使用此編碼配置，空格字元會取代成 x0020 （四位數十六進位碼空格字元）;因此中的資料表名稱 [Order Details][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]變成 _x005B_Order_x0020_Details_x005D\_ XML 中。  
  
 同樣地，您可能需要指定三部分的項目名稱，例如\<[database]。 [擁有者]。[資料表] >。 因為括號字元 （[和]） 都是在 XML 中無效，您必須指定為\<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>，其中 _x005B\_是左括號 ([) 和 _x005D 編碼\_是右括號 (]) 的編碼方式。  
  
## <a name="executing-updategrams"></a>執行 Updategram  
 Updategram 是一個範本，因此，範本的所有處理機制都會套用到 Updategram。 對於 SQLXML 4.0，您可以利用下列任一種方式執行 Updategram：  
  
-   在 ADO 命令中提交它。  
  
-   當做 OLE DB 命令提交它。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
