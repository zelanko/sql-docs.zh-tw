---
title: SQL Server 資料類型和 ADO.NET
description: 說明如何使用 SQL Server 資料類型，及其如何與 .NET 資料類型互動。
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 46edb611f29c447f7e1ca2228212ef3e0d594fff
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244035"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 資料類型和 ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 與 .NET 是以不同的型別系統為基礎，這可能會導致資料遺失。 為維持資料完整性，Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) 提供了可用於處理 SQL Server 資料的具型別存取子方法。 您可以使用 <xref:System.Data.SqlDbType> 類別中的列舉來指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 資料類型。  
  
SQL Server 2008 引進了新的資料類型，其設計目的是為了符合商務需求，以處理日期和時間、結構化、半結構化與非結構化資料。 《SQL Server 2008 線上叢書》中有說明。  
  
可在應用程式中使用的 SQL Server 資料類型，取決於您目前使用的 SQL Server 版本。 如需詳細資訊，請參閱《SQL Server 線上叢書》的[資料類型 (資料庫引擎)](https://go.microsoft.com/fwlink/?LinkID=107468)。
  
## <a name="in-this-section"></a>本節內容  
[SqlTypes 和資料集](sqltypes-dataset.md)  
說明針對 `DataSet` 中的 `SqlTypes` 所提供的類型支援。  
  
[處理 Null 值](handle-null-values.md)  
示範如何處理 Null 值與三值邏輯。  
  
[比較 GUID 和 uniqueidentifier 值](compare-guid-uniqueidentifier-values.md)  
示範如何在 SQL Server 與 .NET 中使用 GUID 與 uniqueidentifier 值。  
  
[日期和時間資料](date-time-data.md)  
描述如何使用 SQL Server 2008 中引進的新日期和時間資料類型。  
  
[大型 UDT](large-udts.md)  
示範如何從 SQL Server 2008 引進的大型值 UDT 擷取資料。  
  
[SQL Server 中的 XML 資料](xml-data-sql-server.md)  
描述如何使用從 SQL Server 擷取的 XML 資料。  
  
## <a name="reference"></a>參考  
<xref:System.Data.DataSet>  
描述 `DataSet` 類別與其所有成員。  
  
<xref:System.Data.SqlTypes>  
描述 `SqlTypes` 命名空間與其所有成員。  
  
<xref:System.Data.SqlDbType>  
描述 `SqlDbType` 列舉與其所有成員。  
  
<xref:System.Data.DbType>  
描述 `DbType` 列舉與其所有成員。  
  
## <a name="next-steps"></a>後續步驟
- [資料表值參數](table-valued-parameters.md)
- [SQL Server 二進位和大型數值資料](sql-server-binary-large-value-data.md)
