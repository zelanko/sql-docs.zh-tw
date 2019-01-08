---
title: 套用 XSL 轉換 （SQLXMLOLEDB 提供者） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74f8834ef29e4b5a1cf2b3988585f771cb9d1f1f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800010"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>套用 XSL 轉換 (SQLXMLOLEDB 提供者)
  在此範例 ADO 應用程式中，會執行 SQL 查詢，而且會將 XSL 轉換套用到結果中。 ClientSideXML 屬性設為 True，就會強制執行用戶端上的資料列集的處理。 命令用語設定為 {5d531cb2-e6ed-11d2-b252-00c04f681b71}，因為 SQL 查詢是在範本中指定，而且此用語必須在執行範本時指定。 Xsl 屬性會指定用來將轉換套用 XSL 檔案。 基底路徑屬性的值用於搜尋 XSL 檔。 如果您指定的 xsl 屬性值中的路徑，路徑會相對於基底路徑屬性中指定的路徑。  
  
 此範例顯示如何使用下列 SQLXMLOLEDB 提供者專屬的屬性：  
  
-   ClientSideXML  
  
-   xsl  
  
 在此用戶端 ADO 範例應用程式中，由 SQL 查詢所組成的 XML 範本會在伺服器上執行。  
  
 ClientSideXML 屬性設定為 True，因為沒有 FOR XML 子句的 SELECT 陳述式會傳送到伺服器。 伺服器會執行查詢，並將資料列集傳回給用戶端。 用戶端接著會將 FOR XML 轉換套用至資料列集，並產生 XML 文件。  
  
 Xsl 指定的屬性是在應用程式中;因此，XSL 轉換套用至用戶端產生的 XML 文件，而且結果為兩個資料行的資料表。  
  
 若要執行 [範本] 命令，就必須指定 XML 範本用語 {-5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此外，這個範例會指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 用於資料提供者 (這需要安裝其他網路用戶端軟體)。 如需詳細資訊，請參閱 < [SQL Server Native Client 的系統需求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
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
  
  
