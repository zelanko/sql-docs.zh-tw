---
title: SqlXmlCommand 物件（SQLXML）
description: 瞭解 SqlXmlCommand 物件的方法和屬性。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c3c3c829b49f52476498e744c91fa5c1af37b6b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767533"
---
# <a name="sqlxml-managed-classes---sqlxmlcommand-object"></a>SQLXML 受控類別 - SqlXmlCommand 物件
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  這是 SqlXmlCommand 物件的構造函式：  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 其中 `cnString` 是用來識別伺服器、資料庫和登入資訊的 ADO 或 OLEDB 連接字串，例如 `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"` 。  
  
 在連接字串中，`Provider` 必須為 SQLOLEDB 而 `Data Provider` 不應包含在連接字串中。  
  
 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
## <a name="methods"></a>方法  
 TheSqlXmlCommand 物件支援數種方法，包括下列執行命令的方法：  
  
 void ExecuteNonQuery （）  
 執行命令，但不會傳回任何東西。 如果您要執行非查詢命令 (也就是不會傳回任何東西的命令)，此方法相當實用。 例如，執行更新記錄但不會傳回任何東西的 Updategram 或 DiffGram。  
  
 Stream ExecuteStream （）  
 傳回新的資料流程物件。 當您希望讓新資料流中的查詢結果傳回給您時，此方法相當實用。 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 public void ExecuteToStream （Stream outputStream）  
 將查詢結果寫入現有的資料流。 當您有需要附加結果的資料流程時（例如，將查詢結果寫入 HttpResponse. OutputStream），這個方法就很有用。 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 XmlReader ExecuteXmlReader （）  
 傳回 XmlReader 物件。 您可以使用這個方法直接操作 XmlReader 物件中的資料，或插入 System.Xml 的可鏈結架構。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 文件集。 如需實用範例，請參閱[使用 ExecuteXMLReader 方法執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)。  
  
 TheSqlXmlCommand 物件也支援下列其他方法：  
  
 SqlXmlParameter CreateParameter （）  
 建立 SqlXmlParameter 物件。 您可以設定這個物件的*Name*和*Value*參數值。 如果您要將參數傳遞到命令，這個方法相當實用。 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 void ClearParameters （）  
 清除針對給定命令物件建立的參數。 如果您要在相同的命令物件上執行多個查詢，這個方法相當實用。  
  
## <a name="properties"></a>屬性  
 SqlXmlCommand 物件也支援下列屬性：  
  
 ClientSideXml  
 設定為 True 時，指定在用戶端而不是伺服器上會將資料列集轉換成 XML。 如果您想要將效能負載移到中介層，這個屬性會很實用。 此屬性也可讓您利用 FOR XML 包裝現有的預存程序來取得 XML 輸出。  
  
 SchemaPath  
 對應結構描述的名稱以及目錄路徑 (例如，C:\x\y\MySchema.xml)。 此屬性對於指定 XPath 查詢的對應結構描述相當實用。 指定的路徑可以是相對或絕對路徑。 如果路徑是相對的，則會使用 [基底路徑] 中所指定的基底路徑來解析相對路徑。 如果未指定基底路徑，相對路徑會相對於目前的目錄。 如需實用範例，請參閱[存取 .Net 環境中的 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 XslPath  
 XSL 檔案的名稱與目錄路徑。 指定的路徑可以是相對或絕對路徑。 如果路徑是相對的，則會使用 [基底路徑] 中所指定的基底路徑來解析相對路徑。 如果未指定基底路徑，相對路徑會相對於目前的目錄。 如需實用範例，請參閱[&#40;SQLXML Managed 類別套用 XSL 轉換&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)。  
  
 基底路徑  
 基底路徑 (目錄路徑)。 這個屬性可用於解析指定給 XSL 檔案的相對路徑（藉由使用 XslPath 屬性）、對應架構檔案（藉由使用 SchemaPath 屬性），或 XML 範本中的外部架構參考（使用**對應架構**屬性指定）。  
  
 OutputEncoding  
 指定命令執行時所傳回之資料流的編碼。 此屬性對於要求所傳回之資料流的特定編碼相當實用。 一些常用的編碼為 UTF-8、ANSI 和 Unicode。 UTF-8 是預設編碼。  
  
 命名空間  
 允許使用命名空間的 XPath 查詢得以執行。 如需使用命名空間之 XPath 查詢的詳細資訊，請參閱[使用命名空間執行 Xpath 查詢 &#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)。 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 XPath 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)。  
  
 RootTag  
 提供命令執行所產生之 XML 的單一根元素。 有效的 XML 文件需要單一根層級標籤。 如果執行的命令產生 XML 片段 (沒有單一最上層元素)，您可以指定傳回之 XML 的根元素。 如需實用範例，請參閱[&#40;SQLXML Managed 類別套用 XSL 轉換&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)。  
  
 CommandText  
 命令的文字。 此屬性對於指定您要執行之命令的文字相當實用。 如需實用範例，請參閱[&#40;SQLXML Managed 類別&#41;執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 CommandStream  
 命令資料流。 如果您要從檔案 (例如，XML 範本) 執行命令，此屬性相當實用。 當您使用 CommandStream 時，只支援「**範本**」、「 **UpdateGram** 」和「 **DiffGram」 CommandType**值。 如需實用範例，請參閱[使用 CommandStream 屬性執行範本](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)檔案。  
  
 CommandType  
 識別命令的類型。 此屬性對於指定您要執行之命令的類型相當實用。 下表中的值會決定命令的類型。 如需實用範例，請參閱[存取 .Net 環境中的 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SqlXmlCommandType .Sql|執行 SQL 命令 (例如，`SELECT * FROM Employees FOR XML AUTO`)。|  
|SqlXmlCommandType XPath|執行 XPath 命令 (例如，`Employees[@EmployeeID=1]`)。|  
|SqlXmlCommandType 範本|執行 XML 範本。|  
|SqlXmlCommandType. TemplateFile|在指定的路徑上執行範本檔案。|  
|SqlXmlCommandType. UpdateGram|執行 Updategram。|  
|SqlXmlCommandType. Diffgram|執行 DiffGram。|  
  
## <a name="see-also"></a>另請參閱  
 [SqlXmlParameter 物件 &#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [SqlXmlAdapter 物件 &#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
