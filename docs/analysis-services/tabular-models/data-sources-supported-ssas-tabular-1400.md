---
title: 支援 SQL Server Analysis Services 表格式 1400年模型中的資料來源 |Microsoft Docs
ms.date: 02/12/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c900c6f1683b9f4c96355a759c604022515d2ce
ms.sourcegitcommit: 89a7bd9ccbcb19bb92a1f4ba75576243a58584e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2019
ms.locfileid: "56159753"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>支援 SQL Server Analysis Services 中表格式 1400年模型的資料來源

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

本文說明適用於 1400年相容性層級的 SQL Server Analysis Services (SSAS) 表格式模型的資料來源的類型。 

為 SSAS 1200 和較低的相容性層級的表格式模型，請參閱[支援 SQL Server Analysis Services 表格式 1200年模型中的資料來源](data-sources-supported-ssas-tabular.md)。

Azure Analysis services，請參閱[支援 Azure Analysis Services 中的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。


## <a name="cloud-data-sources"></a>雲端資料來源

|資料來源  |記憶體中  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   是      |    是      |
|Azure SQL 資料倉儲     |   是      |   是       |
|Azure Blob 儲存體     |   是       |    否      |
|Azure 資料表儲存體    |   是       |    否      |
|Azure Cosmos DB     |  是        |  否        |
|Azure Data Lake Store (Gen1)<sup>[1](#gen2)</sup>      |   是       |    否      |
|Azure HDInsight 的 HDFS    |     是     |   否       |
|Azure HDInsight Spark <sup> [2](#databricks)</sup>     |   是       |   否       |
||||

<a name="gen2">1</a> -目前不支援 ADLS Gen2。   
<a name="databricks">2</a> -azure Databricks 使用的 Spark 連接器目前不支援。   



**提供者**   
記憶體中和連線至 Azure 的資料來源的 DirectQuery 模型中使用.NET Framework Data Provider for SQL Server。

## <a name="on-premises-data-sources"></a>在內部部署資料來源

### <a name="supported-by-in-memory-and-directquery-models"></a>記憶體中和 DirectQuery 模型支援

|資料來源 | 記憶體中的提供者 | DirectQuery 提供者 |
|  --- | --- | --- |
| [SQL Server] |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| SQL Server 資料倉儲 |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| Oracle |Microsoft OLE DB Provider for Oracle, Oracle Data Provider for .NET |適用於.NET 的 oracle 資料提供者 | |
| Teradata |OLE DB Provider for Teradata、 Teradata Data Provider for.NET |Teradata Data Provider for.NET | |
| | | |

> [!NOTE]
> 針對記憶體中模型中，OLE DB 提供者可以提供較佳的效能，大規模的資料。 相同的資料來源的不同提供者之間選擇時，請先嘗試 OLE DB 提供者。  

### <a name="supported-by-in-memory-models-only"></a>支援僅限記憶體中模型

|[資料庫]  |
|---------|---------|---------|
|Access 資料庫     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|JSON 文件     | 
|從二進位檔的行     | 
|MySQL 資料庫     | 
|PostgreSQL 資料庫    | 是 | 否
|SAP HANA   | 是 | 否
|SAP Business Warehouse    | 是 | 否
|Sybase 資料庫     | 是 | 否
|||

|檔案  |  
|---------|---------|
|Excel 活頁簿     |
|資料夾     | 
|JSON | 
|文字/CSV    | 
|XML 表格    | 
|||

|線上服務  |  
|---------|---------|
|Dynamics 365      |
|Exhange Online     |
|Saleforce 物件    | 
|Salesforce 報表     |
|SharePoint Online 清單     |
|||

|其他  |  
|---------|---------|
|Active Directory      | 
|Exhange     |  
|OData 摘要     | 
|ODBC 查詢     | 
|OLE DB  | 
|SharePoint 清單 | 
|||

## <a name="see-also"></a>另請參閱

[支援 SQL Server Analysis Services 中表格式 1200年模型的資料來源](data-sources-supported-ssas-tabular.md)

[支援 Azure Analysis Services 中的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
