---
title: 錯誤介面中的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 460a0a2cf58d5980b1265db91d053e3088b55a99
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704979"
---
# <a name="information-in-error-interfaces"></a>錯誤介面中的資訊
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會在 OLE DB 定義的錯誤介面**IErrorInfo**、 **IErrorRecords**和**ISQLErrorInfo**中，報告一些錯誤和狀態資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援**IErrorInfo**成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**GetSource**|字串 "Microsoft SQL Server Native Client"。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援取用者可用的**IErrorRecords**成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在 **ISQLErrorInfo** 和 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 介面上傳回參考。|  
|**GetErrorInfo**|在 **IErrorInfo** 介面上傳回參考。|  
|**GetErrorParameters**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者不會透過**GetErrorParameters**將參數傳回給取用者。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援**ISQLErrorInfo：： GetSQLInfo**參數，如下所示。  
  
|參數|說明|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 都不 OLE DB 提供者定義的執行特定 SQLSTATE 值。|  
|*plNativeError*|從 **master.dbo.sysmessages** 傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤號碼 (如果有的話)。 成功初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料來源之後，就可以使用原生錯誤。 在嘗試之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](errors.md)  
  
  
