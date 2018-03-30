---
title: SQL Server 的 OLE DB 驅動程式 |Microsoft 文件
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL 或 OLE DB 驅動程式會針對 SQL Server 是一個詞彙，已交換用來參考 SQL Server 的 OLE DB 驅動程式。

## <a name="different-incarnations-of-ole-db-drivers"></a>OLE DB 驅動程式的不同 Incarnations

有三個相異的多采 for SQL Server 的 Microsoft OLE DB 提供者。


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)

[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍然隨附於[Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx)。 不建議使用這個驅動程式，開發新項目。


### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC，)

在 SQL Server 2005 中，啟動[SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供者介面 (SQLNCLI)，並隨附於 SQL Server 2005 中透過 SQL Server 2017 的 OLE DB 提供者。

它是[宣佈將被取代，在 2011年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)也不建議使用這個驅動程式，開發新項目。


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.SQL Server (MSOLEDBSQL) 的 Microsoft OLE DB 驅動程式

OLE DB 已[推出，在 2017 undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)。 新的已規劃的發行已宣布的 2018年。

新的 OLE DB 提供者會呼叫 Microsoft OLE DB 驅動程式的 SQL Server (MSOLEDBSQL)。 新的提供者將會更新為最新的伺服器功能，從現在開始使用。

SQL Server 功能，OLE DB 驅動程式的資訊︰

-   [SQL Server Support for LocalDB 的 OLE DB 驅動程式](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [中繼資料探索](../oledb/features/metadata-discovery.md)  

-   [SQL Server 的 OLE DB 驅動程式中的 utf-16 支援](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [高可用性、 災害復原的 SQL Server 支援的 OLE DB 驅動程式](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [存取擴充事件記錄檔中的診斷資訊](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 的 OLE DB 驅動程式](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [SQL Server 功能的 OLE DB 驅動程式](../oledb/features/oledb-driver-for-sql-server-features.md )  
