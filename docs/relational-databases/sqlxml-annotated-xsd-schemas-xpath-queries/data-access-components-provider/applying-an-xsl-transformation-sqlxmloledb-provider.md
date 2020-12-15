---
title: '將 XSL 轉換套用 (SQLXMLOLEDB) '
description: 瞭解如何使用 SQLXMLOLEDB 提供者的 ClientSideXML 和 xsl 屬性，在 ADO 應用程式中套用 XSL 轉換。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13b34c51cf1d963613cab47455e718d6b46c8f5b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479249"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>套用 XSL 轉換 (SQLXMLOLEDB 提供者)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  在此範例 ADO 應用程式中，會執行 SQL 查詢，而且會將 XSL 轉換套用到結果中。 將 ClientSideXML 屬性設定為 True 會強制處理用戶端上的資料列集。 命令用語設定為 {5d531cb2-e6ed-11d2-b252-00c04f681b71}，因為 SQL 查詢是在範本中指定，而且此用語必須在執行範本時指定。 Xsl 屬性會指定要用來套用轉換的 XSL 檔。 [基底路徑] 屬性的值是用來搜尋 XSL 檔案。 如果您在 [xsl] 屬性的值中指定路徑，則路徑會相對於 [基底路徑] 屬性中指定的路徑。  
  
 此範例顯示如何使用下列 SQLXMLOLEDB 提供者專屬的屬性：  
  
-   ClientSideXML  
  
-   xsl  
  
 在此用戶端 ADO 範例應用程式中，由 SQL 查詢所組成的 XML 範本會在伺服器上執行。  
  
 因為 ClientSideXML 屬性設定為 True，所以不含 FOR XML 子句的 SELECT 語句會傳送至伺服器。 伺服器會執行查詢，並將資料列集傳回給用戶端。 用戶端接著會將 FOR XML 轉換套用至資料列集，並產生 XML 文件。  
  
 Xsl 屬性是在應用程式中指定;因此，XSL 轉換會套用到在用戶端上產生的 XML 檔，而結果會是兩個數據行的資料表。  
  
 若要執行範本命令，必須指定 XML 範本方言-{5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此外，這個範例會指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 用於資料提供者 (這需要安裝其他網路用戶端軟體)。 如需詳細資訊，請參閱 [SQL Server Native Client 的系統需求](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 XSL 範本如下。 套用此 XSL 範本的結果為兩個資料行的資料表。  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
