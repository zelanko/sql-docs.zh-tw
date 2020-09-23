---
title: ISSAbort::Abort (OLE DB 驅動程式) | Microsoft Docs
description: 了解 ISSAbort::Abort 方法如何取消目前的資料列集，以及與 OLE DB Driver for SQL Server 中的目前命令相關聯的任何批次命令。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18e8c8544c557292bd5a7cc813d809ea0f9cf061
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860070"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
在 OLE DB Driver for SQL Server 中公開的 `ISSAbort` 介面會提供 `ISSAbort::Abort` 方法，可用於取消目前的資料列集加上使用命令批次處理的任何命令，此命令一開始會產生資料列集，而且尚未完成執行。  
  
 `ISSAbort` 是 OLE DB Driver for SQL Server 特定的介面，可以使用 `ICommand::Execute` 或 `IOpenRowset::OpenRowset` 所傳回之 `IMultipleResults` 物件上的 `QueryInterface` 取得。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會終止。 如果伺服器正在將結果集傳送到用戶端，將會停止傳送。 如果用戶端不想要使用結果集，可以呼叫 `**`ISSAbort::Abort` before releasing the rowset will speed up the rowset release, but if there is an open transaction and XACT_ABORT is ON, the transaction will be rolled back when `ISSAbort::Abort`  
  
 `ISSAbort::Abort` 傳回 S_OK 之後，相關聯的 `IMultipleResults` 介面會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 `IUnknown` 介面所定義的方法之外)，直到釋放它為止。 如果在呼叫 `Abort` 前已經從 `IMultipleResults` 取得 `IRowset`，它也會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 `IUnknown` 介面和 `IRowset::ReleaseRows` 所定義的方法以外)，直到成功呼叫 `ISSAbort::Abort` 後釋放它為止。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，如果伺服器 XACT_ABORT 狀態為 ON，執行 `ISSAbort::Abort` 會終止並回復連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的任何目前隱含或明確交易。 舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 `ISSAbort::Abort` 方法會傳回 S_OK，如果批次遭到取消，則為 DB_E_CANTCANCEL。 如果批次已經遭到取消，就會傳回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 批次已經遭到取消。  
  
 DB_E_CANTCANCEL  
 批次未取消。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，物件會因為已經呼叫 `ISSAbort::Abort` 而處於廢止狀態。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
  
