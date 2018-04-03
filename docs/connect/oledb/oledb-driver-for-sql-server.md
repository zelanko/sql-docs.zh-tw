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
ms.openlocfilehash: fbc52a9e982da45586ce7ace5e58e8985869e552
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2018
---
# <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL 或 OLE DB 驅動程式的 SQL Server，是指 OLE DB 驅動程式將 SQL Server 的交換使用的詞彙。

## <a name="different-generations-of-ole-db-drivers"></a>不同的層代的 OLE DB 驅動程式

有三個不同的層代的 SQL Server 的 Microsoft OLE DB 提供者。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍然隨附於[Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx)。 它不會再保留並不建議使用這個驅動程式，開發新項目。 


### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC，)
從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供者介面 (SQLNCLI)，並隨附的 OLE DB 提供者[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]透過[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。

它是[宣佈將被取代，在 2011年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)也不建議使用這個驅動程式，開發新項目。 如需可用的下載與 SNAC 生命週期的詳細資訊，請參閱[所說明的 SNAC 生命週期](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.SQL Server (MSOLEDBSQL) 的 Microsoft OLE DB 驅動程式
OLE DB 已[undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)和發行 2018，而且可以在下載[這裡](https://go.microsoft.com/fwlink/?linkid=871294)。

新的 OLE DB 提供者會呼叫 Microsoft OLE DB 驅動程式的 SQL Server (MSOLEDBSQL)。 新的提供者將會更新為最新的伺服器功能，從現在開始使用。

> [!NOTE]
> 若要使用 SQL Server，新 Microsoft OLE DB 驅動程式中現有的應用程式，您應該規劃將連接字串從 SQLOLEDB 或 SQLNCLI，轉換成 MSOLEDBSQL。   

SQL Server 功能，OLE DB 驅動程式的資訊︰

-   [OLE DB Driver for SQL Server 支援 LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [中繼資料探索](../oledb/features/metadata-discovery.md)  

-   [OLE DB Driver for SQL Server 中支援 UTF-16](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [OLE DB Driver for SQL Server 支援高可用性、災害復原](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [存取擴充事件記錄檔中的診斷資訊](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 的 OLE DB 驅動程式](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[OLE DB Driver for SQL Server 功能](../oledb/features/oledb-driver-for-sql-server-features.md )     
