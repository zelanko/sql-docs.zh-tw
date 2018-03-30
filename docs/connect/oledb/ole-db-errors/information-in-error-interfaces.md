---
title: 錯誤介面中的資訊 |Microsoft 文件
description: 錯誤介面中的資訊
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
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
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36cfb611737570e0d2a0d2774a0306706bfe5c6a
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式報告一些錯誤和狀態的資訊，在 OLE DB 定義的錯誤介面**IErrorInfo**， **IErrorRecords**，和**ISQLErrorInfo**。  
  
 SQL Server 的 OLE DB 驅動程式支援**IErrorInfo**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**Ierrorinfo**|字串 「 Microsoft OLE DB 驅動程式的 SQL Server 」。|  
  
 SQL Server 的 OLE DB 驅動程式支援取用者可用**IErrorRecords**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在介面上傳回參考**ISQLErrorInfo**和[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)。|  
|**GetErrorInfo**|上傳回參考**IErrorInfo**介面。|  
|**GetErrorParameters**|SQL Server OLE DB 驅動程式不會將參數傳回給取用者透過**GetErrorParameters**。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 SQL Server 的 OLE DB 驅動程式支援**:: Getsqlinfo<**參數，如下所示。  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 既不[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或 SQL Server OLE DB 驅動程式會定義實作特定的 SQLSTATE 值。|  
|*isqlerrorinfo:: Getsqlinfo*|傳回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]錯誤號碼**master.dbo.sysmessages**的話。 成功地嘗試初始化 OLE DB 驅動程式的 SQL Server 資料來源之後，就可以使用原生的錯誤。 在該項嘗試之前 SQL Server OLE DB 驅動程式一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
