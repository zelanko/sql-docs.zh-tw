---
title: 使用計算資料行升級 XML 值 | Microsoft Docs
description: 了解如何透過建立計算資料行來提升經常使用的 XML 值，以進行更有效率的查詢。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: c5881835f6a415b47825181d7d5a74ec24677e3c
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891938"
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>使用計算資料行升級常用的 XML 值
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  如果查詢主要只是針對少數的元素和屬性值來執行，您可能會想要將那些量升級至關聯式資料行。 若已擷取整個 XML 執行個體，但您只是要針對小部分的 XML 資料來發出查詢要求時，這是很有幫助的。 您不需要在 XML 資料行上建立 XML 索引， 即可為升級的資料行建立索引。 您必須撰寫查詢來使用升級的資料行。 意即，查詢最佳化工具不再將 XML 資料行查詢的目標放在升級的資料行。  
  
 升級的資料行可以是同一資料表中的已計算資料行，也可以是資料表中由使用者維護的另一個資料行。 當單一值從每個 XML 執行個體升級起來時，這就足夠了。 然而，若為多重值的屬性，您就必須為屬性建立個別的資料表，請見下節說明。  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>以 xml 資料類型為基礎的計算的資料行  
 您可以使用叫用 **xml** 資料類型方法的使用者定義函數，進而建立計算資料行。 計算資料行的類型可以是任何 SQL 類型，包括 XML。 下列範例會加以說明。  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>範例：以 xml 資料類型方法為基礎的計算資料行  
 針對書籍的 ISBN 號碼來建立使用者自訂函數：  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 將計算的資料行加入 ISBN 的資料表中：  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 可以用一般的方式來檢索計算的資料行。  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>範例：查詢以 xml 資料類型方法為基礎的計算資料行  
 若要取得 ISBN 為 0-7356-1588-2 的 <`book`>，請：  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 您可以改寫對 XML 資料行的查詢，以使用計算的資料行，如下所示：  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 您可以建立使用者定義函數，以使用該使用者定義函數來傳回 **xml** 資料類型和計算的資料行。 然而，您不能在計算的 XML 資料行上建立 XML 索引。  
  
## <a name="creating-property-tables"></a>建立屬性資料表  
 您可能會想要將某些多重值的屬性從 XML 資料升級至一或多個資料表中、在那些資料表上建立索引，然後再讓您的查詢目標使用那些資料表。 一般案例中都是由少數的屬性來涵蓋大部份的查詢工作負載。 您可以執行下列工作：  
  
-   建立一或多個資料表來保存多重值的屬性。 您會發現，每個資料表各儲存一個屬性，並且在屬性資料表中複製基底資料表的主索引鍵，再向後聯結基底資料表，這麼做是很方便的。  
  
-   如果您要維持屬性的相對順序，就必須為相對順序導入另一個資料行。  
  
-   在 XML 資料行上建立觸發程序，以維護屬性資料表。 在觸發程序中執行下列其中之一：  
  
    -   使用 **xml** 資料類型方法，例如： **nodes()** 和 **value()** ，進而插入及刪除屬性資料表的資料列。  
  
    -   在 Common Language Runtime (CLR) 中建立資料流資料表值函式，以插入及刪除屬性資料表的資料列。  
  
    -   撰寫查詢來讓 SQL 存取屬性資料表，並讓 XML 存取基底資料表中的 XML 資料表，再使用其主索引鍵來聯結這二個資料表。  
  
### <a name="example-create-a-property-table"></a>範例：建立屬性資料表  
 舉例來說，假設您要升級作者的名字。 書籍的作者可能不只一個，所以名字是多重值的屬性。 每個名字都是儲存在屬性資料表的不同資料列中。 在屬性資料表中會複製基底資料表的主索引鍵，以供向後聯結。  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>範例：建立使用者自訂函數，以從 XML 執行個體產生資料列集  
 下列資料表值函式 udf_XML2Table 可接受主索引鍵值和 XML 執行個體。 它會擷取 <`book`> 元素中所有作者的名字，並傳回主索引鍵的資料列集 (名字配對)。  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>範例：建立觸發程序以填入屬性資料表  
 插入觸發程序會在屬性資料表中插入資料列：  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 刪除觸發程序會依據已刪除之資料列的主索引鍵值，從屬性資料表中刪除資料列：  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 更新觸發程序會在對應至已更新之 XML 執行個體的屬性資料表中，刪除現有的資料列，並且在屬性資料表中插入新的資料列：  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>範例：尋找作者名字相同的 XML 執行個體  
 查詢可以在 XML 資料行上形成。 或者，可以在屬性資料表中搜尋 "David" 這個名字，然後執行向後聯結基底資料表，以傳回 XML 執行個體。 例如：  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>範例：使用 CLR 資料流資料表值函式的解決方案  
 這個解決方案包含下列步驟：  
  
1.  定義 CLR 類別 SqlReaderBase，在 XML 執行個體上套用路徑運算式，以實作 ISqlReader 並產生資料流資料表值的輸出。  
  
2.  建立組件及 Transact-SQL 使用者自訂函數，以啟動 CLR 類別。  
  
3.  使用使用者自訂函數來定義插入、更新及刪除觸發程序，以維護屬性資料表。  

 若要執行此作業，您要先建立資料流 CLR 函數。 **xml** 資料類型在 ADO.NET 中公開為 Managed 類別 SqlXml，並支援傳回 XmlReader 的 **CreateReader()** 方法。  
  
> [!NOTE]  
>  本節中的範例程式碼使用 XPathDocument 及 XPathNavigator。 它們會強制您將所有 XML 文件載入記憶體。 如果您在應用程式中使用類似的程式碼來處理好幾個大型 XML 文件，此程式碼是無法調整的。 反之，您要讓記憶體配置維持少量，並且盡可能使用資料流介面。 如需有關效能的詳細資訊，請參閱 [CLR 整合的架構](../clr-integration/clr-integration-architecture-clr-hosted-environment.md)。  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 接著，請建立組件以及對應於 CLR 函數 streaming_xml_tvf 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者自訂函數 SQL_streaming_xml_tvf (未顯示)。 使用者自訂函數可用來定義資料表值函式 CLR_udf_XML2Table，以產生資料列集：  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 最後，請依照範例「建立觸發程序來擴展屬性資料表」的說明來定義觸發程序，但請將 udf_XML2Table 置換成 CLR_udf_XML2Table 函數。 插入觸發程序如下列範例中所示：  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 刪除觸發程序與非 CLR 版本相同。 然而，更新觸發程序只會將函數 udf_XML2Table() 置換成 CLR_udf_XML2Table()。  
  
## <a name="see-also"></a>另請參閱  
 [使用計算資料行中的 XML](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
