---
description: OLE DB 定義的錯誤介面中的資訊
title: 錯誤介面中的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71e8c8187cb9e70e32e3c29deaf1e3a9bd912c94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465288"
---
# <a name="information-in-ole-db-defined-error-interfaces"></a>OLE DB 定義的錯誤介面中的資訊
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會在 OLE DB 定義的錯誤介面**IErrorInfo**、 **IErrorRecords**和**ISQLErrorInfo**中，報告一些錯誤和狀態資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者支援**IErrorInfo**成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetDescription**|描述性的錯誤訊息字串。|  
|**GetGUID**|定義錯誤之介面的 GUID。|  
|**GetHelpContext**|不支援。 永遠傳回零。|  
|**GetHelpFile**|不支援。 一律傳回 NULL。|  
|**GetSource**|字串 "Microsoft SQL Server Native Client"。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者支援取用者可用的**IErrorRecords**成員函式，如下所示。  
  
|成員函數|描述|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|以有關錯誤的基本資訊填入 ERRORINFO 結構。 ERRORINFO 結構所包含的成員會識別錯誤的 HRESULT 傳回值，以及該錯誤適用的提供者和介面。|  
|**GetCustomErrorObject**|在 **ISQLErrorInfo** 和 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 介面上傳回參考。|  
|**GetErrorInfo**|在 **IErrorInfo** 介面上傳回參考。|  
|**GetErrorParameters**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者不會透過**GetErrorParameters**將參數傳回給取用者。|  
|**GetRecordCount**|可用錯誤記錄的計數。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB provider 支援**ISQLErrorInfo：： GetSQLInfo**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pbstrSQLState*|為錯誤傳回 SQLSTATE 值。 SQLSTATE 值定義於 SQL-92、ODBC 和 ISO SQL，以及 API 規格中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端和原生用戶端都不 OLE DB 提供者定義的實 SQLSTATE 值。|  
|*plNativeError*|從 **master.dbo.sysmessages** 傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤號碼 (如果有的話)。 嘗試初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者資料來源後，就可以使用原生錯誤。 在嘗試之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者一律會傳回零。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
