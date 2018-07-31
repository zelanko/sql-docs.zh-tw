---
title: 錯誤介面中的資訊 |Microsoft Docs
description: 錯誤介面中的資訊
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3f5b9334beae9c3a65c290adffae1075788191c4
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106024"
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會在 OLE DB 定義的錯誤介面 **IErrorInfo**、**IErrorRecords** 和 **ISQLErrorInfo** 中，報告一些錯誤和狀態資訊。  
  
 OLE DB Driver for SQL Server 支援**IErrorInfo**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**GetSource**|字串 "Microsoft OLE DB Driver for SQL Server"。|  
  
 OLE DB Driver for SQL Server 支援取用者可用**IErrorRecords**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在 **ISQLErrorInfo** 和 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面上傳回參考。|  
|**GetErrorInfo**|在 **IErrorInfo** 介面上傳回參考。|  
|**GetErrorParameters**|OLE DB Driver for SQL Server 不會將參數傳回給取用者透過**GetErrorParameters**。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 OLE DB Driver for SQL Server 支援**isqlerrorinfo:: Getsqlinfo**參數，如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 既不[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或 OLE DB Driver for SQL Server 定義實作特定的 SQLSTATE 值。|  
|*plNativeError*|從 **master.dbo.sysmessages** 傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤號碼 (如果有的話)。 在成功地嘗試初始化 OLE DB Driver for SQL Server 資料來源之後，就可以使用原生的錯誤。 嘗試之前，SQL Server OLE DB 驅動程式一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
