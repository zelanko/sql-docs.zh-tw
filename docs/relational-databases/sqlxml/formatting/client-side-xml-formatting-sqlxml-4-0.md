---
title: 用戶端 XML 格式化 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- middle tier XML formatting [SQLXML]
- client-side XML formatting
- client-side-xml attribute
ms.assetid: 9630a21d-a93b-4d3b-8a25-c4b32399f993
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 95ed0b26f885474b87b45addd08dfcdb67b4bff9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62503715"
---
# <a name="client-side-xml-formatting-sqlxml-40"></a>用戶端 XML 格式 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題提供有關用戶端 XML 格式的資訊。 用戶端格式指的是 XML 在中間層的格式。  
  
> [!NOTE]  
>  本主題提供在用戶端上使用 FOR XML 子句的其他資訊，並假設您已經熟悉 FOR XML 子句。 如需有關 FOR XML 的詳細資訊，請參閱 <<c0> [ 使用 FOR XML 建構 XML](../../../relational-databases/xml/for-xml-sql-server.md)。  
  
 **重要**若要使用用戶端 FOR XML 功能與新**xml**資料型別，用戶端應該永遠會使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (SQLNCLI11) 資料提供者，而非 SQLOLEDB 提供者。 SQLNCLI11 是最新版的 SQL Server 提供者，而且完全了解 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 推出的資料類型。 FOR XML 搭配 SQLOLEDB 提供者會將用戶端的行為**xml**為字串資料類型。  
  
## <a name="formatting-xml-documents-on-the-client-side"></a>格式化用戶端上的 XML 文件  
 當用戶端應用程式執行下列查詢時：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML RAW  
```  
  
 只有查詢的這個部分會傳送到伺服器：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 伺服器會執行查詢，並傳回給用戶端的資料列集 （其中包含 FirstName 和 LastNamecolumns）。 中間層接著會將 FOR XML 轉換套用至資料列集，並將 XML 格式傳回到用戶端。  
  
 同樣地，當您執行 XPath 查詢時，伺服器會將資料列集傳回到用戶端，並將 FOR XML EXPLICIT 轉換套用到用戶端上的資料列集，以產生所需的 XML 格式。  
  
 下表顯示您利用用戶端 FOR XML 指定的模式。  
  
|用戶端 FOR XML 模式|註解|  
|-------------------------------|-------------|  
|RAW|在用戶端或伺服器端的 FOR XML 中指定時，會產生相同的結果。|  
|NESTED|這類似於伺服器端上的 FOR XML AUTO 模式。|  
|EXPLICIT|這類似於伺服器端的 FOR XML EXPLICIT 模式。|  
  
> [!NOTE]  
>  如果您指定 AUTO 模式並要求用戶端 XML 格式，會將完整的查詢傳送到伺服器，也就是說，XML 格式會出現在伺服器上。 這是為了方便而進行，但是請注意，NESTED 模式會傳回基礎資料表名稱，當做所產生之 XML 文件中的元素名稱。 您撰寫的部分應用程式可能需要基礎資料表名稱。 例如，您可能會執行一個預存程序，並將所產生的資料載入到資料集 (在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中)，接著在稍後產生 DiffGram 來更新資料表中的資料。 在此種情況下，您需要基礎資料表資訊，而且您必須使用 NESTED 模式。  
  
## <a name="benefits-of-client-side-xml-formatting"></a>用戶端 XML 格式的優點  
 以下為在用戶端上格式化 XML 的一些優點。  
  
### <a name="if-you-have-stored-procedures-on-the-server-that-return-a-single-rowset-you-can-request-client-side-for-xml-transformation-to-generate-an-xml"></a>如果您在伺服器上的預存程序傳回單一資料列集，您可以要求用戶端 FOR XML 轉換產生 XML。  
 例如，請考慮下列預存程序。 此預存程序會先從 AdventureWorks 資料庫的 Person.Contact 資料表中，傳回員工的名字和姓氏。  
  
```  
IF EXISTS (SELECT name FROM sysobjects  
   WHERE name = 'GetContacts' AND type = 'P')  
   DROP PROCEDURE GetContacts  
GO  
CREATE PROCEDURE GetContacts  
AS  
    SELECT   FirstName, LastName  
    FROM     Person.Contact  
```  
  
 下列範例 XML 範本會執行預存程序。 FOR XML 子句會在預存程序名稱後指定。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    EXEC GetContacts FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 因為**用戶端端 xml**屬性在範本中設為 1 (true)、 在伺服器上執行預存程序和伺服器所傳回的兩個資料行資料列集是中介層上轉換成 XML，並傳回給用戶端。 (此處僅顯示部分結果)。  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact FirstName="Catherine" LastName="Abel" />  
</ROOT>  
```  
  
> [!NOTE]  
>  當您使用的是 SQLXMLOLEDB 提供者或 SQLXML Managed 類別時，您可以使用**ClientSideXml**屬性來要求用戶端 XML 格式。  
  
### <a name="the-workload-is-more-balanced"></a>工作負載較為對稱。  
 由於用戶端會執行 XML 格式化，因此在伺服器和用戶端之間的工作負載較為對稱，讓伺服器可以做其他的事情。  
  
## <a name="supporting-client-side-xml-formatting"></a>支援用戶端 XML 格式  
 為支援用戶端 XML 格式功能，SQLXML 提供：  
  
-   SQLXMLOLEDB 提供者  
  
-   SQLXML Managed 類別  
  
-   增強的 XML 範本支援  
  
-   SqlXmlCommand.ClientSideXml 屬性  
  
     您可以將 SQLXML Managed 類別的這個屬性設定為 true，藉以指定用戶端功能。  
  
## <a name="enhanced-xml-template-support"></a>增強的 XML 範本支援  
 開頭[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]中的 XML 範本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加上已增強**用戶端端 xml**屬性。 如果此屬性設定為 true，XML 會在用戶端上格式化。 請注意，此範本屬性的功能與 SQLXMLOLEDB 提供者專屬 ClientSideXML 屬性相同。  
  
> [!NOTE]  
>  如果您正在使用 SQLXMLOLEDB 提供者的 ADO 應用程式中執行 XML 範本，而且您同時指定**用戶端端 xml**範本和提供者 ClientSideXML 屬性中指定的值中的屬性範本會優先使用。  
  
## <a name="see-also"></a>另請參閱  
 [用戶端和伺服器端 XML 格式化架構&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)   
 [FOR XML 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [xml 在 SQLXML 4.0 中的資料類型支援](../../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)   
 [SQLXML Managed 類別](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)   
 [用戶端和伺服器端 XML 格式化&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-vs-server-side-xml-formatting-sqlxml-4-0.md)   
 [SqlXmlCommand 物件&#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [XML 資料 &#40;SQL Server&#41;](../../../relational-databases/xml/xml-data-sql-server.md)  
  
  
