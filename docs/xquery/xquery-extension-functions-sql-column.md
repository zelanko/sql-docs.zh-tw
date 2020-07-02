---
title: sql： column （）函數（XQuery） |Microsoft Docs
description: 瞭解 XQuery 函數 sql： column （）如何用來系結 XML 內的非 XML 關聯式資料，並將關聯式和 XML 資料整合在一起。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b3aeded0476c809bd1bcdfbfdacb4eac3381751
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775413"
---
# <a name="xquery-extension-functions---sqlcolumn"></a>XQuery 擴充函式 - sql:column()
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  如在 XML 內系結[關聯式資料](../t-sql/xml/binding-relational-data-inside-xml-data.md)主題中所述，當您使用[Xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)來公開 XQuery 內的關聯式值時，可以使用**sql： column （（）** 函數。  
  
 例如， [query （）方法（XML 資料類型）](../t-sql/xml/query-method-xml-data-type.md)是用來針對儲存在**xml**類型之變數或資料行中的 xml 實例指定查詢。 有時，您可能會想要讓查詢使用另一個非 XML 資料行的值，以同時查詢關聯式資料與 XML 資料。 若要這樣做，您可以使用**sql： column （）** 函數。  
  
 SQL 值將會對應到一個相對應的 XQuery 值，且其類型會是等同於相對應 SQL 類型的 XQuery 基底類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>備註  
 請注意，在 XQuery 內**sql： column （）** 函數中指定之資料行的參考，是指正在處理之資料列中的資料行。  
  
 在中 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，您只能參考 xml-DML insert 語句之來源運算式內容中的**xml**實例; 否則，您不能參考**xml**類型或 CLR 使用者定義類型的資料行。  
  
 聯結作業中不支援**sql： column （）** 函數。 可改為使用 APPLY 作業。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>A. 使用 sql:column() 來擷取 XML 內的關聯式值  
 在建構 XML 時，下列範例說明如何擷取非 XML 關聯式資料行的值，以繫結 XML 與關聯式資料。  
  
 此查詢建構具有下列格式的 XML：  
  
```xml
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 請注意在建構 XML 中的下列項目：    
  
-   **ProductID**、 **ProductName**和**ProductPrice**屬性值是從**Product**資料表取得。  
  
-   **ProductModelID**屬性值是從**ProductModel**資料表中抓取。  
  
-   為了讓查詢更有趣，會從**xml 類型**的**CatalogDescription**資料行取得**ProductModelName**屬性值。 由於並非所有的產品型號都有儲存 XML 產品型號目錄資訊，因此 `if` 陳述式可用以擷取存在的值。  
  
    ```sql
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   因為值是從兩個不同的資料表擷取而來，所以 FROM 子句會指定兩個資料表。 WHERE 子句中的條件會篩選結果，並只擷取產品型號含有目錄描述的產品。  
  
-   [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的**namespace**關鍵字會定義在查詢主體中使用的 XML 命名空間前置詞 "pd"。 請注意資料表別名 "P" 與 "PM" 是定義在查詢本身的 FROM 子句中。  
  
-   **Sql： column （）** 函數是用來將非 xml 值帶入 xml 內部。  
  
 以下是部份結果：  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 下列查詢建構了包含產品特定資訊的 XML。 此資訊包含隸屬於特定產品型號 ProductModelID=19 的所有產品之 ProductID、ProductName、ProductPrice 以及 ProductModelName (如果有的話)。 然後會將 XML 指派給 @x **xml**類型的變數。  
  
```sql
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server XQuery 擴充功能函式](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [比較具類型的 XML 與不具類型的 XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [建立 XML 資料的執行個體](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
