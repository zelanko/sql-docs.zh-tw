---
title: 'ISSAbort:: Abort (OLE DB) |Microsoft Docs'
description: ISSAbort::Abort (OLE DB)
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 72ce7fa29adfb349fab8c9e60872740c94484108
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994392"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
在 OLE DB Driver for SQL Server 中公開的 **ISSAbort** 介面會提供 **ISSAbort::Abort** 方法，可用於取消目前的資料列集加上使用命令批次處理的任何命令，此命令一開始會產生資料列集，而且尚未完成執行。  
  
 **ISSAbort** 是 OLE DB Driver for SQL Server 特定的介面，可以使用 **ICommand::Execute** 或 **IOpenRowset::OpenRowset** 所傳回之 **IMultipleResults** 物件上的 **QueryInterface** 取得。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會終止。 如果伺服器正在將結果集傳送到用戶端，將會停止傳送。 如果用戶端不想要取用結果集，在釋放資料列集前呼叫 **ISSAbort::Abort** 將會加速資料列集的釋放，但是如果有開啟的交易，而且 XACT_ABORT 為 ON，呼叫 **ISSAbort::Abort** 時，將會回復交易  
  
 **ISSAbort::Abort** 傳回 S_OK 之後，相關聯的 **IMultipleResults** 介面會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 **IUnknown** 介面所定義的方法之外)，直到釋放它為止。 如果在呼叫 **Abort** 前已經從 **IMultipleResults** 取得 **IRowset**，它也會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 **IUnknown** 介面和 **IRowset::ReleaseRows** 所定義的方法以外)，直到成功呼叫 **ISSAbort::Abort** 後釋放它為止。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，如果伺服器 XACT_ABORT 狀態為 ON，執行 **ISSAbort::Abort** 會終止並回復連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的任何目前隱含或明確交易。 舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 **ISSAbort::Abort** 方法會傳回 S_OK，如果批次遭到取消，則為 DB_E_CANTCANCEL。 如果批次已經遭到取消，就會傳回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 批次已經遭到取消。  
  
 DB_E_CANTCANCEL  
 批次未取消。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，物件會因為已經呼叫 **ISSAbort::Abort** 而處於廢止狀態。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
  
