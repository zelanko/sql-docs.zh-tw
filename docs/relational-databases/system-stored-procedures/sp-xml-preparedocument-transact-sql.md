---
title: sp_xml_preparedocument （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 56468767e60d49d0fc92864cd613a4f36e84132a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67950521"
---
# <a name="sp_xml_preparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  讀取以輸入提供的 XML 文字、使用 MSXML 剖析器 (Msxmlsql.dll) 剖析文字，以及以隨時可取用的狀態來提供已剖析的文件。 這份已剖析的文件是以樹狀表示 XML 文件中的不同節點：元素、屬性、文字、註解等等。  
  
 **sp_xml_preparedocument**會傳回可用來存取新建立之 xml 檔內部表示的控制碼。 這個控制碼在會話的持續時間內有效，或在控制碼因執行**sp_xml_removedocument**而失效之前。  
  
> [!NOTE]  
>  經過剖析的文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部快取中。 MSXML 剖析器會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用總記憶體的八分之一。 若要避免記憶體不足，請執行**sp_xml_removedocument**以釋放記憶體。  
  
> [!NOTE]  
>  為了回溯相容性， **sp_xml_preparedocument**會在屬性中折迭 CR （char （13））和 LF （char （10））字元，即使這些字元是實體化的。  
  
> [!NOTE]  
>  **Sp_xml_preparedocument**所叫用的 XML 剖析器可以剖析內部 dtd 和實體宣告。 由於惡意結構化的 Dtd 和實體宣告可用來執行阻絕服務攻擊，因此強烈建議使用者不要直接將不受信任來源的 XML 檔傳遞給**sp_xml_preparedocument**。  
>   
>  為了減輕遞迴實體擴充攻擊， **sp_xml_preparedocument**限制為10000可在檔最上層的單一實體底下展開的實體數目。 這項限制並不適用於字元或數值實體。 此限制允許儲存含有多個實體參考的文件，但是會妨止超過 10,000 個擴充之鏈結中的實體進行遞迴擴充。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**會將一次可以開啟的專案數限制為256。  

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
 這是新建立之文件的控制代碼。 *hdoc*是整數。  
  
 [ *xmltext* ]  
 這是原始 XML 文件集。 MSXML 剖析器會剖析這份 XML 文件。 *xmltext*是文字參數： **char**、 **Nchar**、 **Varchar**、 **Nvarchar**、 **text**、 **Ntext**或**xml**。 預設值是 NULL，在這個情況下，會建立空白 XML 文件的內部表示法。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**只能處理文字或不具類型的 xml。 若要作為輸入使用之執行個體值是具類型的 XML，請先將它轉換為新的不具類型的 XML 執行個體，或轉換為字串，然後以輸入形式傳遞該值。 如需詳細資訊，請參閱[比較具類型的 xml 與](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)不具類型的 xml。  
  
 [ *xpath_namespaces* ]  
 指定使用於 OPENXML 中之資料列和資料行 XPath 運算式中的命名空間宣告。 *xpath_namespaces*是文字參數： **char**、 **Nchar**、 **Varchar**、 **Nvarchar**、 **text**、 **Ntext**或**xml**。  
  
 預設值為** \<root xmlns： mp = "urn：架構-microsoft-com： xml-xml-metaprop" >**。 *xpath_namespaces*會藉由格式正確的 XML 檔，提供 OPENXML 中 xpath 運算式中使用之前置詞的命名空間 uri。 *xpath_namespaces*宣告必須用來參考命名空間**urn：架構-microsoft-com： xml-xml-metaprop**; 的前置詞。這會提供有關已剖析之 XML 元素的中繼資料。 雖然您可以使用這個技巧來重新定義中繼屬性命名空間的命名空間前置詞，但不會失去這個命名空間。 前置詞**mp**仍然適用于**urn：架構-microsoft-com： xml-xml-metaprop** ，即使*xpath_namespaces*不含這類宣告。  
  
## <a name="return-code-values"></a>傳回碼值  
 0（成功）或 >0 （失敗）  
  
## <a name="permissions"></a>權限  
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
 下列範例會傳回以輸入形式提供之 XML 文件新建內部表示法的控制代碼。 的呼叫會`sp_xml_preparedocument`保留中繼`mp`屬性命名空間對應的前置詞，並`xyz`將對應前置詞加入`urn:MyNamespace`命名空間。  
  
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
 <br>[XML 預存程式（Transact-sql）](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[系統預存程式（Transact-sql）](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML （Transact-sql）](../../t-sql/functions/openxml-transact-sql.md)
 <br>[sys.databases dm_exec_xml_handles （Transact-sql）](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  
