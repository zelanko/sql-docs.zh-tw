---
title: sp_xml_preparedocument (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 50235db46a664d1507823c057dc0cb61eda90974
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980048"
---
# <a name="spxmlpreparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  讀取以輸入提供的 XML 文字、使用 MSXML 剖析器 (Msxmlsql.dll) 剖析文字，以及以隨時可取用的狀態來提供已剖析的文件。 這份已剖析的文件是以樹狀表示 XML 文件中的不同節點：元素、屬性、文字、註解等等。  
  
 **sp_xml_preparedocument**傳回的控制代碼，可用來存取 XML 文件的新建內部表示法。 這個控制代碼的有效時間為工作階段，或直到控點無效的執行持續時間**sp_xml_removedocument**。  
  
> [!NOTE]  
>  經過剖析的文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部快取中。 MSXML 剖析器會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用總記憶體的八分之一。 若要避免記憶體不足，請執行**sp_xml_removedocument**以釋出記憶體。  
  
> [!NOTE]  
>  針對回溯相容性**sp_xml_preparedocument**摺疊的 CR （char(13 和 LF （即使這些字元實體化的屬性中的 char(10)) 個字元。  
  
> [!NOTE]  
>  XML 剖析器所叫用**sp_xml_preparedocument**可以剖析內部 Dtd 和實體宣告。 因為惡意建構的 Dtd 和實體宣告可用來執行阻斷服務攻擊，我們強烈建議，使用者不是直接將 XML 文件傳遞從受信任的來源**sp_xml_preparedocument**。  
>   
>  若要減輕遞迴實體擴充攻擊**sp_xml_preparedocument**文件的高層級的單一實體之下可以擴充的實體數目限制為 10,000。 這項限制並不適用於字元或數值實體。 此限制允許儲存含有多個實體參考的文件，但是會妨止超過 10,000 個擴充之鏈結中的實體進行遞迴擴充。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**限制為 256 一次可以開啟的項目數。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_xml_preparedocument  
hdoc   
OUTPUT  
[ , xmltext ]  
[ , xpath_namespaces ]   
```  
  
## <a name="arguments"></a>引數  
 *hdoc*  
 這是新建立之文件的控制代碼。 *hdoc*是一個整數。  
  
 [ *xmltext* ]  
 這是原始 XML 文件集。 MSXML 剖析器會剖析這份 XML 文件。 *xmltext*是文字參數： **char**， **nchar**， **varchar**， **nvarchar**，**文字**， **ntext**或是**xml**。 預設值是 NULL，在這個情況下，會建立空白 XML 文件的內部表示法。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**只能處理文字或不具類型的 XML。 若要作為輸入使用之執行個體值是具類型的 XML，請先將它轉換為新的不具類型的 XML 執行個體，或轉換為字串，然後以輸入形式傳遞該值。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
 [ *xpath_namespaces* ]  
 指定使用於 OPENXML 中之資料列和資料行 XPath 運算式中的命名空間宣告。 *xpath_namespaces*是文字參數： **char**， **nchar**， **varchar**， **nvarchar**，**文字**， **ntext**或是**xml**。  
  
 預設值是 **\<根 xmlns:mp ="urn: schemas-microsoft-microsoft-schemas-microsoft-com:-xml-metaprop">** 。 *xpath_namespaces*提供透過語式正確的 XML 文件在 OPENXML 中 XPath 運算式中使用的前置詞的命名空間 Uri。 *xpath_namespaces*宣告必須用來參考命名空間前置詞**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-xml-metaprop**; 它提供有關已剖析之 XML 元素的中繼資料。 雖然您可以使用這個技巧來重新定義中繼屬性命名空間的命名空間前置詞，但不會失去這個命名空間。 前置詞**mp**仍適用於**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-xml-metaprop**即使*xpath_namespaces*包含沒有這類宣告。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 （成功） 或 > 0 （失敗）  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>A. 準備格式正確之 XML 文件的內部表示法  
 下列範例會傳回以輸入形式提供之 XML 文件新建內部表示法的控制代碼。 在呼叫 `sp_xml_preparedocument` 時，使用預設命名空間前置詞對應。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
-- Remove the internal representation.  
exec sp_xml_removedocument @hdoc;  
```  
  
### <a name="b-preparing-an-internal-representation-for-a-well-formed-xml-document-with-a-dtd"></a>B. 準備具有 DTD 的格式正確之 XML 文件的內部表示法  
 下列範例會傳回以輸入形式提供之 XML 文件新建內部表示法的控制代碼。 預存程序會針對以文件中包含的 DTD 來驗證載入的文件。 在呼叫 `sp_xml_preparedocument` 時，使用預設命名空間前置詞對應。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(2000);  
SET @doc = '  
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE root   
[<!ELEMENT root (Customers)*>  
<!ELEMENT Customers EMPTY>  
<!ATTLIST Customers CustomerID CDATA #IMPLIED ContactName CDATA #IMPLIED>]>  
<root>  
<Customers CustomerID="ALFKI" ContactName="Maria Anders"/>  
</root>';  
  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
```  
  
### <a name="c-specifying-a-namespace-uri"></a>C. 指定命名空間 URI  
 下列範例會傳回以輸入形式提供之 XML 文件新建內部表示法的控制代碼。 在呼叫`sp_xml_preparedocument`會保留`mp`中繼屬性命名空間對應前置詞，並將`xyz`命名空間的對應前置詞`urn:MyNamespace`。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc, '<ROOT xmlns:xyz="urn:MyNamespace"/>';  
```  
  
## <a name="see-also"></a>另請參閱  
 <br>[XML 預存 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[系統預存 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML(Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
 <br>[sys.dm_exec_xml_handles (Transact-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  
