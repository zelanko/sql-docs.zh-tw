---
title: "比較具類型的 XML 與不具類型的 XML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27533bcc63a8df64597db4529b16a26f1fb5a009
ms.lasthandoff: 04/11/2017

---
# <a name="compare-typed-xml-to-untyped-xml"></a>比較具類型的 XML 與不具類型的 XML
  您可以建立 **XML** 類型的變數、參數和資料行。 此外，也可以選擇性地將 XML 結構描述的集合與 **XML** 類型的變數、參數和資料行建立關聯。 在此情況下，此 **XML** 資料類型的執行個體即稱為「具類型」**。 非此種情況下的 XML 執行個體則稱為「不具類型」**。  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>格式正確的 XML 和 xml 資料類型  
 **XML** 資料類型會實作 ISO 標準 **XML** 資料類型。 因此，它可以在不具類型的 XML 資料行中儲存格式良好的 XML 1.0 版文件，也可以儲存含有文字節點和任意數量之最上層元素的所謂 XML 內容片段。 系統會確認資料的格式良好、不需要將資料行繫結到 XML 結構描述，並拒絕在某種程度上格式不良的資料。 對於不具類型的 XML 變數和參數而言，也是如此。  
  
## <a name="xml-schemas"></a>XML 結構描述  
 XML 結構描述提供下列項目：  
  
-   **驗證的條件約束** ：每當指派或修改了具類型的 xml 執行個體，SQL Server 就會驗證該執行個體。  
  
-   **資料類型資訊** 結構描述會提供 **XML** 資料類型執行個體中屬性和元素類型的相關資訊。 這些類型資訊針對執行個體中所包含之值所提供的運算語意，要比不具類型的 **XML**更精確。 例如，十進位的數學運算可以在十進位值上執行，但不能在字串值上執行。 因此，具類型的 XML 儲存會比不具類型的 XML 精簡很多。  
  
## <a name="choosing-typed-or-untyped-xml"></a>選擇具類型或不具類型的 XML  
 在下列情況下，請使用不具類型的 **XML** 資料類型：  
  
-   您沒有 XML 資料的結構描述。  
  
-   您有結構描述，但您不想讓伺服器驗證資料。 當應用程式在將資料儲存於伺服器之前執行用戶端驗證時，或是根據結構描述暫時儲存無效的 XML 資料時，或是在伺服器上使用不受支援的結構描述元件時，有時會有這種情形。  
  
 在下列情況下，請使用具類型的 **XML** 資料類型：  
  
-   您有 XML 資料的結構描述，而且想要讓伺服器根據該 XML 結構描述來驗證 XML 資料。  
  
-   您想要依據類型資訊來利用儲存體及查詢最佳化作業。  
  
-   您想要在編譯查詢期間更有效地利用類型資訊。  
  
 具類型的 XML 資料行、參數及變數可儲存 XML 文件或內容。 但是您必須在宣告時，用旗標來指定您是要儲存文件還是內容。 此外，您也必須提供 XML 結構描述的集合。 如果每個 XML 執行個體都只有一個最上層元素，請指定 DOCUMENT。 否則，請使用 CONTENT。 查詢編譯器會在查詢編譯期間，於類型檢查中使用 DOCUMENT 旗標，以推斷單一最上層元素。  
  
## <a name="creating-typed-xml"></a>建立具類型的 XML  
 您必須先使用 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 註冊 XML 結構描述集合之後，才能夠建立具類型的 **XML** 變數、參數或資料行。 然後，您可以將 XML 結構描述集合與 **XML** 資料類型的變數、參數或資料行產生關聯。  
  
 在下列範例中，會使用兩段式命名慣例來指定 XML 結構描述集合名稱。 第一個部分是結構描述名稱，而第二個部分是 XML 結構描述集合名稱。  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>範例：將結構描述集合與 xml 類型變數產生關聯  
 下列範例會建立一個**XML** 類型變數，並將結構描述集合與此變數產生關聯。 範例中指定的結構描述集合已經匯入 **AdventureWorks** 資料庫。  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>範例：指定 xml 類型資料行的結構描述  
 下列範例會建立具有 **XML** 類型資料行的資料表，並為此資料行指定結構描述：  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>範例：將 xml 類型的參數傳遞給預存程序  
 下列範例會將 **XML** 類型的參數傳遞給預存程序，並為此變數指定結構描述：  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 請注意下列有關 XML 結構描述集合的項目：  
  
-   XML 結構描述集合只適用於使用 [建立 XML 結構描述集合](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)來註冊它的資料庫。  
  
-   如果您將字串轉換成具類型的 **XML** 資料類型，則剖析作業也會根據所指定之集合中的 XML 結構描述命名空間來執行驗證和設定類型。  
  
-   您可以將具類型的 **XML** 資料類型轉換為不具類型的 **XML** 資料類型，反之亦然。  
  
 如需在 SQL Server 中產生 XML 之其他方法的詳細資訊，請參閱 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)。 在產生 XML 之後，可將它指派給 **XML** 資料類型的變數，或將它儲存在 **XML** 類型資料行中，以進行其他處理。  
  
 在資料類型階層中， **XML** 資料類型會出現在 **sql_variant** 和使用者定義類型的下面，但會出現在任何內建類型的上面。  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>範例：指定 Facet 來約束 xml 類型的資料行  
 對於具類型的 **XML** 資料行而言，您可以約束資料行，讓儲存在其中的每個執行個體只能有單一的最上層元素。 作法是，在建立資料表時指定選擇性的 `DOCUMENT` Facet，如下列範例所示：  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 依預設，儲存在具類型的 **XML** 資料行中的執行個體會儲存為 XML 內容，而非 XML 文件。 這樣做可允許有下列項目：  
  
-   零個或者許多最上層元素  
  
-   最上層元素內的文字節點  
  
 您也可以藉由加入 `CONTENT` Facet，明確指定此行為，如下列範例所示：  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 請注意，您可以在任何定義 **XML** 類型 (具類型的 XML) 的地方，指定選擇性的 DOCUMENT/CONTENT Facet。 例如，當您建立具類型的 **XML** 變數時，可以加入 DOCUMENT/CONTENT Facet，如下所示：  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>文件類型定義 (DTD)  
 **XML** 資料類型資料行、變數及參數可以用 XML 結構描述來設定類型，但不能用 DTD 來設定。 但是，內嵌 DTD 可用於不具類型和具類型的 XML 來提供預設值，並將實體參考取代為其展開的形式。  
  
 您可以用協力廠商工具將 DTD 轉換成 XML 結構描述文件，並將 XML 結構描述載入資料庫中。  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>從 SQL Server 2005 升級具類型的 XML  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 對於 XML 結構描述支援做了幾項擴充，其中包括支援 Lax 驗證，改進 **xs:date**、 **xs:time** 和 **xs:dateTime** 執行個體資料的處理，並加入了清單和聯集類型的支援。 在大多數情況下，這些變更並不會影響升級的使用體驗。 但是，如果您在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中使用允許 **xs:date**、 **xs:time**或 **xs:dateTime** 類型 (或任何子類型) 值的 XML 結構描述集合，則當您將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加到更新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，會進行下列升級步驟：  
  
1.  對於每一個 XML 資料行而言，如果它在 XML 結構描述集合中具類型 (該集合包含的元素或屬性具有 **xs:anyType**、 **xs:anySimpleType**、 **xs:date** 類型或它的任何子類型、 **xs:time** 或它的任何子類型或是 **xs:dateTime** 或它的任何子類型)，或是為包含這些類型之任何一項的聯集或清單類型時，會發生下列情況：  
  
    1.  資料行上的所有 XML 索引都將會停用。  
  
    2.  所有的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 值都將會繼續以 Z 時區來表示，因為這些值已經正規化成 Z 時區。  
  
    3.  在下列情況下，任何小於 1 年 1 月 1 日的 **xs:date** 或 **xs:dateTime** 值都會導致發生執行階段錯誤：當重建索引時，或是針對包含該值的 XML 資料類型執行 XQuery 或 XML-DML 陳述式時。  
  
2.  **xs:date** 或 **xs:dateTime** Facet 中的任何負數年份或是 XML 結構描述集合中的預設值，將會自動更新為基底 **xs:date** 或 **xs:dateTime** 類型所允許的最小值 (例如 **xs:dateTime**的 0001-01-01T00:00:00.0000000Z)。  
  
 請注意，您仍然可以使用簡單 SQL SELECT 陳述式來擷取整個 XML 資料類型，即使它包含負數年份。 建議您使用新支援範圍中的年份來取代負數年份，或是將元素或屬性的類型變更為 **xs:string**。  
  
## <a name="see-also"></a>另請參閱  
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
