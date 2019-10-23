---
title: OLE DB Driver for SQL Server 的支援原則 | Microsoft Docs
description: OLE DB Driver for SQL Server 的支援原則
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381864"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的支援原則
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文討論如何在 SQL Server 的 OLE DB 驅動程式中使用各種資料存取元件。  

## <a name="server-support"></a>伺服器支援  
 SQL Server 的 OLE DB 驅動程式支援透過 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 連接。

## <a name="supported-operating-system-versions"></a>支援的作業系統版本  
 下表列出哪些作業系統支援 SQL Server 的 OLE DB 驅動程式。  

| 支援的作業系統 |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [2014 年4月更新](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 +[四月2014更新](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>ADO 支援原則  
 如果 ADO 應用程式不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的任何功能，就可以使用 Windows 隨附的 SQLOLEDB OLE DB 提供者。  

 ADO 應用程式可以使用 SQL Server 的 OLE DB 驅動程式，但如果它們這麼做，就必須在連接字串中指定 `DataTypeCompatibility=80`。 當連接字串中存在 `DataTypeCompatibility=80` 時，只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  

## <a name="ole-db-support-policies"></a>OLE DB 支援原則  
應用程式應該使用 Windows 作業系統隨附的 OLE DB 提供者 (SQLOLEDB)。 不過，這處於維護模式，且不再更新。 請改用 SQL Server 的 OLE DB 驅動程式（內含 MSOLEDBSQL.H）。

## <a name="see-also"></a>另請參閱  
 [使用 OLE DB Driver for SQL Server 建置應用程式](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
