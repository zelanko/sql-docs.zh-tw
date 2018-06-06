---
title: 錯誤介面中的資訊 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6687b4dbc8dd0a47c3e2116b27e814240463cc90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會報告一些錯誤和狀態資訊在 OLE DB 定義的錯誤介面**IErrorInfo**， **IErrorRecords**，和**ISQLErrorInfo**.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援**IErrorInfo**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**Ierrorinfo**|字串 "Microsoft SQL Server Native Client"。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援取用者可用**IErrorRecords**成員函式，如下所示。  
  
|成員函數|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在介面上傳回參考**ISQLErrorInfo**和[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)。|  
|**GetErrorInfo**|上傳回參考**IErrorInfo**介面。|  
|**GetErrorParameters**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不會將參數傳回給取用者透過**GetErrorParameters**。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援 **:: Getsqlinfo<** 參數，如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 既不[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會定義實作特定的 SQLSTATE 值。|  
|*isqlerrorinfo:: Getsqlinfo*|傳回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤號碼**master.dbo.sysmessages**的話。 成功地嘗試初始化之後就可以使用原生錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料來源。 在該項嘗試之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
