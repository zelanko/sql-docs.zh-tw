---
title: 錯誤介面中的資訊
description: OLE DB Driver for SQL Server 會在 OLE DB 定義的錯誤介面 IErrorInfo、IErrorRecords 和 ISQLErrorInfo 中，報告一些錯誤和狀態資訊。
ms.custom: ''
ms.date: 05/06/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7651d01bef5b17981c0e4c93c450f26e7970524d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081917"
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會在 OLE DB 定義的錯誤介面 **IErrorInfo**、**IErrorRecords** 和 **ISQLErrorInfo** 中，報告一些錯誤和狀態資訊。  
  
 OLE DB Driver for SQL Server 支援 **IErrorInfo** 成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**GetSource**|字串 "Microsoft OLE DB Driver for SQL Server"。|  
  
 OLE DB Driver for SQL Server 支援取用者可用的 **IErrorRecords** 成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在 **ISQLErrorInfo** 和 [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) 介面上傳回參考。|  
|**GetErrorInfo**|在 **IErrorInfo** 介面上傳回參考。|  
|**GetErrorParameters**|OLE DB Driver for SQL Server 不會透過 **GetErrorParameters** 將參數傳回取用者。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 OLE DB Driver for SQL Server 支援 **ISQLErrorInfo::GetSQLInfo** 參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 OLE DB Driver for SQL Server 都沒有定義實作特定的 SQLSTATE 值。|  
|*plNativeError*|從 **master.dbo.sysmessages** 傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤號碼 (如果有的話)。 在成功地嘗試初始化 OLE DB Driver for SQL Server 資料來源後，就可以使用原生錯誤。 在該項嘗試之前，OLE DB Driver for SQL Server 一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
