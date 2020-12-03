---
title: OLE DB Driver for SQL Server 的支援原則
description: 了解適用於 OLE DB Driver for SQL Server 的支援原則，以及每個驅動程式版本所支援的作業系統與 SQL 資料庫版本。
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa01dec4758bb91a4b05d65af372ee66c1c53672
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506417"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的支援原則
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

此文章討論如何搭配 OLE DB Driver for SQL Server 使用各種資料存取元件。  

## <a name="sql-version-support"></a>SQL 版本支援  

OLE DB Driver for SQL Server 已經過測試，並支援下列 SQL Server 版本的連線。

| 資料庫版本&nbsp;&#8594;<br />&#8595; 驅動程式版本 | Azure SQL Database | Azure Synapse Analytics | Azure SQL 受控執行個體 | SQL Server 2019 | SQL Server 2017 | SQL Server 2016 | SQL Server 2014 | SQL Server 2012 |
|----|---|---|---|---|---|---|---|---|
|18.5|是|是|是|是|是|是|是|是|
|18.4|是|是|是|是|是|是|是|是|
|18.3|是|是|是|是|是|是|是|是|
|18.2|是|是|是|是|是|是|是|是|
|18.1|是|是|是|   |是|是|是|是|
|18.0|是|是|是|   |是|是|是|是|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="supported-operating-system-versions"></a>支援的作業系統版本  

下表列出 OLE DB Driver for SQL Server 支援哪些作業系統。  

| 作業系統&nbsp;&#8594;<br />&#8595; 驅動程式版本 | Windows Server 2019 | Windows Server 2016 | Windows Server 2012<sup>1</sup> | Windows Server 2012 R2<sup>2</sup> | Windows 10 | Windows 8.1<sup>3</sup> |
|----|---|---|---|---|---|---|
|18.5|是|是|是|是|是|是|
|18.4|是|是|是|是|是|是|
|18.3|是|是|是|是|是|是|
|18.2|是|是|是|是|是|是|
|18.1|   |是|是|是|是|是|
|18.0|   |是|是|是|是|是|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> 支援 Windows Server 2012 (含 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061))。  
<sup>2</sup> 支援 Windows Server 2012 R2 (含 [2014 年 4 月更新](https://go.microsoft.com/fwlink/?linkid=2073785)和 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061))。  
<sup>3</sup> 支援 Windows 8.1 (含 [2014 年 4 月更新](https://go.microsoft.com/fwlink/?linkid=2073785)和 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061))。  

## <a name="ado-support-policies"></a>ADO 支援原則  

如果 ADO 應用程式不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的任何功能，就可以使用 Windows 隨附的 SQLOLEDB OLE DB 提供者。  

ADO 應用程式可以使用 OLE DB Driver for SQL Server，但是使用時，必須在連接字串中指定 `DataTypeCompatibility=80`。 當連接字串中存在 `DataTypeCompatibility=80` 時，只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  

## <a name="ole-db-support-policies"></a>OLE DB 支援原則  

應用程式應該使用 Windows 作業系統隨附的 OLE DB 提供者 (SQLOLEDB)。 不過，這處於維護模式，且不再更新。 請改為使用 OLE DB Driver for SQL Server (MSOLEDBSQL)。

## <a name="see-also"></a>另請參閱  

[使用 OLE DB Driver for SQL Server 建置應用程式](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)
