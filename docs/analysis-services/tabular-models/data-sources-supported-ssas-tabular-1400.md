---
title: 支援 SQL Server Analysis Services 表格式 1400年模型中的資料來源 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b511ac6d9cf4d75faddf569fcc2391317f19629
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>支援 SQL Server Analysis Services 中表格式 1400年模型的資料來源

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

這篇文章描述可以搭配 SQL Server Analysis Services (SSAS) 1400年相容性層級的表格式模型的資料來源的類型。 

SSAS 1200 或更低的相容性層級的表格式模型，請參閱[支援 SQL Server Analysis Services 表格式 1200年模型中的資料來源](data-sources-supported-ssas-tabular.md)。

Azure Analysis Services，請參閱[支援 Azure Analysis Services 中的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。


## <a name="cloud-data-sources"></a>雲端資料來源

|Azure 的資料來源  |記憶體中  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   是      |    是      |
|Azure SQL 資料倉儲     |   是      |   是       |
|Azure Blob 儲存體     |   是       |    否      |
|Azure 資料表儲存體    |   是       |    否      |
|Azure Cosmos DB      |  是        |  否        |
|Azure Data Lake Store     |   是       |    否      |
|Azure HDInsight HDFS     |     是     |   否       |
|Azure HDInsight Spark (Beta)     |   是       |   否       |
||||

**提供者**   
記憶體中和 DirectQuery 模型連接到 Azure 的資料來源使用.NET Framework Data Provider for SQL Server。

## <a name="on-premises-data-sources"></a>在內部部署資料來源

### <a name="supported-by-in-memory-and-directquery-models"></a>記憶體中和 DirectQuery 模型支援

|資料來源 | 記憶體中的提供者 | DirectQuery 的提供者 |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| SQL Server 資料倉儲 |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| Oracle |Microsoft OLE DB Provider for Oracle，適用於.NET 的 Oracle 資料提供者 |適用於.NET 的 oracle 資料提供者 | |
| Teradata |OLE DB Provider for Teradata，適用於.NET 的 Teradata 資料提供者 |適用於.NET 的 Teradata 資料提供者 | |
| | | |

> [!NOTE]
> 記憶體中模型的 OLE DB 提供者可以提供較佳的效能，大型的資料。 相同的資料來源的不同提供者之間選擇時，請先嘗試 OLE DB 提供者。  

### <a name="supported-by-in-memory-models-only"></a>記憶體中模式只支援

|資料庫  |
|---------|---------|---------|
|Access 資料庫     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|JSON 文件     | 
|從二進位檔的線條     | 
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
|線上 Exhange     |
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

[Azure Analysis Services 中支援的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
