---
title: SQL XML 資料行值
description: 示範如何擷取及使用從 SQL Server 擷取出來的 XML 資料。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: aa02072e139c2446ae67086ef43668af4403890c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244006"
---
# <a name="sql-xml-column-values"></a>SQL XML 資料行值

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 支援 `xml` 資料類型，開發人員可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 類別的標準行為擷取包含此類型的結果集。 `xml` 資料行的擷取方式就如同擷取任何資料行 (例如，擷取到 <xref:Microsoft.Data.SqlClient.SqlDataReader>)，但如果您想要將資料行的內容當做 XML 使用，則必須使用 <xref:System.Xml.XmlReader>。  
  
## <a name="example"></a>範例  
下列主控台應用程式會從 **AdventureWorks** 資料庫中的 **Sales.Store** 資料表，選取兩個資料列 (每個資料列包含一個 `xml` 資料行) 至 <xref:Microsoft.Data.SqlClient.SqlDataReader> 執行個體中。 針對每個資料列，會使用 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 方法來讀取 `xml` 資料行的值。 此值會儲存於 <xref:System.Xml.XmlReader>。 請注意，如果您想要將內容設定為 <xref:System.Data.SqlTypes.SqlXml> 變數，就必須使用 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A>，而不是 <xref:System.Data.IDataRecord.GetValue%2A> 方法；<xref:System.Data.IDataRecord.GetValue%2A> 會以字串形式傳回 `xml` 資料行的值。  
  
> [!NOTE]
>  當您安裝 SQL Server 時，預設不會安裝 **AdventureWorks** 範例資料庫。 您可以執行 SQL Server 安裝程式加以安裝。  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>後續步驟
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server 中的 XML 資料](xml-data-sql-server.md)
