---
title: 執行 SQL 查詢 （SQLXMLOLEDB 提供者） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d6c6ce6b2876ac713ad8b71131685e7791f5747
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209514"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>執行 SQL 查詢 (SQLXMLOLEDB 提供者)
  此範例示範如何使用下列 SQLXMLOLEDB 提供者專屬的屬性：  
  
-   ClientSideXML  
  
-   xml root  
  
 在此用戶端的 ADO 範例應用程式中，會在用戶端上執行簡單的 SQL 查詢。 ClientSideXML 屬性設定為 True，因為沒有 FOR XML 子句的 SELECT 陳述式會傳送到伺服器。 伺服器會執行查詢，並將資料列集傳回給用戶端。 用戶端接著會將 FOR XML 轉換套用至資料列集，並產生 XML 文件。  
  
 Xml root 屬性就會產生 XML 文件提供單一最上層的根項目。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此外，這個範例會指定針對資料提供者使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) (需要安裝其他網路用戶端軟體)。 如需詳細資訊，請參閱 < [SQL Server Native Client 的系統需求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
