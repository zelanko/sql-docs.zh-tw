---
title: "建立 XML 資料類型變數與資料行 | Microsoft Docs"
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
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 751fccc2a458239715c187a1925046cdf74de98a
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-xml-data-type-variables-and-columns"></a>建立 XML 資料類型變數與資料行
  **xml** 資料類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的內建資料類型，而且與其他內建類型有些相似，例如 **int** 與 **varchar**。 如同其他內建類型，當您建立資料表作為變數類型、參數類型、函數傳回類型，或是在 **CAST 和 CONVERT** 中建立資料表時，可以使用 [xml](../../t-sql/functions/cast-and-convert-transact-sql.md)資料類型作為資料行類型。  
  
## <a name="creating-columns-and-variables"></a>建立資料行和變數  
 若要在資料表中建立 `xml` 類型資料行，請使用 `CREATE TABLE` 陳述式，如下列範例所示：  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 您可以使用 `DECLARE statement` 來建立 `xml` 類型的變數，如下列範例所示。  
  
```  
DECLARE @x xml   
```  
  
 藉由指定 XML 結構描述集合來建立具類型的 `xml` 變數，如下列範例所示。  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 若要將 `xml` 類型參數傳遞給預存程序，請使用 `CREATE PROCEDURE` 陳述式，如下列範例所示。  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 您可以使用 XQuery 來查詢儲存在資料行、參數或變數中的 XML 執行個體中。 您也可以使用「XML 資料操作語言」(XML DML) 來套用 XML 執行個體的更新。 由於 XQuery 標準在開發時並不會定義 XQuery DML，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引進了 XQuery 的 [XML 資料修改語言](../../t-sql/xml/xml-data-modification-language-xml-dml.md) 擴充功能。 這些延伸模組可讓您執行插入、更新和刪除作業。  
  
## <a name="assigning-defaults"></a>指派預設值  
 在資料表中，您可以將預設的 XML 執行個體指派給 **xml** 類型的資料行。 您可以使用以下兩種方法的其中一種來提供預設的 XML：使用 XML 常數，或是明確轉換成 **xml** 類型。  
  
 若要將預設 XML 提供為 XML 常數，請使用類似以下範例的語法。 請注意，此字串會隱含轉換成 **xml** 類型。  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 若要將預設 XML 提供為轉換成 `CAST` 的明確 `xml`，請使用類似以下範例的語法。  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援在 **xml** 類型之資料行上的 NULL 和 NOT NULL 條件約束。 例如：  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>指定條件約束  
 當您建立 **xml** 類型的資料行時，您可以定義資料行層級或資料表層級的條件約束。 在下列情況下，請使用條件約束：  
  
-   您的商務規則無法以 XML 結構描述來表達。 例如，花店的送貨地址必須在該店的方圓 50 英哩內。 這一點可以在 XML 資料行上寫成條件約束。 條件約束可能會牽涉到 **xml** 資料類型方法。  
  
-   您的條件約束牽涉到資料表中的其他 XML 或非 XML 資料行。 有一個例子，就是強制 XML 執行個體中的「客戶識別碼」(`/Customer/@CustId`) 要符合關聯式 CustomerID 資料行中的值。  
  
 您可以為具類型或不具類型的 **xml** 資料類型資料行指定條件約束。 不過，在指定條件約束時無法使用 [XML 資料類型方法](../../t-sql/xml/xml-data-type-methods.md) 。 此外，請注意 **xml** 資料類型不支援下列資料行和資料表條件約束：  
  
-   PRIMARY KEY/ FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     XML 可自行提供編碼。 定序僅適用於字串類型。 **xml** 資料類型不是字串類型。 但它確實具有字串表示法，並允許轉換成字串資料類型，以及從字串資料類型轉換回來。  
  
-   RULE  
  
 有一個替代使用條件約束的方法就是建立包裝函式 (用來包裝 **xml** 資料類型方法的使用者定義函數)，並在檢查條件約束中指定使用者定義函數，如下列範例所示。  
  
 在下列範例中，在 `Col2` 上的條件約束指定儲存在此資料行中的每個 XML 執行個體都必須有包含 `<ProductDescription>` 屬性的 `ProductID` 元素。 此條件約束是由使用者定義函數所強制執行：  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 請注意如果在執行個體中的 `exist()` 元素包含 `xml` 屬性， `1` 資料類型的 `<ProductDescription>` 方法會傳回 `ProductID` 。 否則會傳回 `0`。  
  
 現在，您可以使用下列資料行層級的條件約束來建立資料表：  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 下列插入會成功：  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 由於條件約束之故，下列插入會失敗：  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>相同或相異的資料表  
 **xml** 資料類型資料行可以建立在含有其他關聯式資料行的資料表中，或是建立在與主資料表有外部索引鍵關聯性的另一個資料表中。  
  
 若下列其中一種情況成立，請將 **xml** 資料類型資料行建立在同一個資料表中：  
  
-   您的應用程式在 XML 資料行上執行資料擷取，而且不需要 XML 資料行的 XML 索引。  
  
-   您想要在 **xml** 資料類型資料行上建立 XML 索引，且主資料表的主索引鍵與其叢集索引鍵相同。 如需詳細資訊，請參閱 [XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)。  
  
 若下列情況成立，請將 **xml** 資料類型資料行建立在不同的資料表中：  
  
-   您想要在 **xml** 資料類型資料行上建立 XML 索引，但是主資料表的主索引鍵與其叢集索引鍵不同、主資料表沒有主索引鍵，或者主資料表是堆積 (沒有叢集索引鍵)。 如果主資料表已存在，就可能會有這種情形。  
  
-   您不想因為資料表中有 XML 資料行存在，而讓資料表掃描的速度慢下來。 無論是以同資料列或資料列外的方式儲存，都會用到空間。  
  
  
