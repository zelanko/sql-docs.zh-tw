---
title: 錯誤介面中的資訊 |Microsoft Docs
description: 錯誤介面中的資訊
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ff18864e37575f78d129abb1569b0ffe83d4685
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994939"
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會在 OLE DB 定義的錯誤介面 **IErrorInfo**、**IErrorRecords** 和 **ISQLErrorInfo** 中，報告一些錯誤和狀態資訊。  
  
 SQL Server 的 OLE DB 驅動程式支援**IErrorInfo**成員函式, 如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**GetSource**|字串 "Microsoft OLE DB Driver for SQL Server"。|  
  
 SQL Server 的 OLE DB 驅動程式支援取用者可用的**IErrorRecords**成員函式, 如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在 **ISQLErrorInfo** 和 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面上傳回參考。|  
|**GetErrorInfo**|在 **IErrorInfo** 介面上傳回參考。|  
|**GetErrorParameters**|SQL Server 的 OLE DB 驅動程式不會透過**GetErrorParameters**將參數傳回給取用者。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 SQL Server 的 OLE DB 驅動程式支援**ISQLErrorInfo:: GetSQLInfo**參數, 如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 驅動程式都不適用 SQL Server 定義的執行特定 SQLSTATE 值。|  
|*plNativeError*|從 **master.dbo.sysmessages** 傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤號碼 (如果有的話)。 成功初始化 SQL Server 資料來源的 OLE DB 驅動程式之後, 就可以使用原生錯誤。 在嘗試之前, SQL Server 的 OLE DB 驅動程式一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
