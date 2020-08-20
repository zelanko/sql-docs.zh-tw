---
description: 'ISSAbort：： Abort (Native Client OLE DB provider) '
title: ISSAbort：： Abort (Native Client OLE DB provider) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 392d02ccff41fa3ab7d1ab50fa6801279b1b18f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490836"
---
# <a name="issabortabort-native-client-ole-db-provider"></a>ISSAbort：： Abort (Native Client OLE DB Provider) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
在 Native Client OLE DB provider 中公開的 **ISSAbort** 介面 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 **ISSAbort：： Abort** 方法，可用來取消目前的資料列集，加上以初始產生資料列集的命令批次處理的任何命令，而且尚未完成執行。  
  
 **ISSAbort**是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端提供者特定介面，可透過**ICommand：： Execute**或**IOpenRowset：： OpenRowset**所傳回之**IMultipleResults**物件上的**QueryInterface**來使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程式中， (預存程式的執行，以及任何已呼叫該程式) 的程式將會終止，以及包含預存程序呼叫的命令批次。 如果伺服器正在將結果集傳送到用戶端，將會停止這個動作。 如果用戶端不想要取用結果集，在釋放資料列集前呼叫 **ISSAbort::Abort** 將會加速資料列集的釋放，但是如果有開啟的交易，而且 XACT_ABORT 為 ON，呼叫 **ISSAbort::Abort** 時，將會回復交易  
  
 **ISSAbort::Abort** 傳回 S_OK 之後，相關聯的 **IMultipleResults** 介面會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 **IUnknown** 介面所定義的方法之外)，直到釋放它為止。 如果在呼叫 **Abort** 前已經從 **IMultipleResults** 取得 **IRowset**，它也會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 **IUnknown** 介面和 **IRowset::ReleaseRows** 所定義的方法以外)，直到成功呼叫 **ISSAbort::Abort** 後釋放它為止。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，如果伺服器 XACT_ABORT 狀態為 ON，執行 **ISSAbort::Abort** 會終止並回復連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何目前隱含或明確交易。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
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
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，物件會因為已經呼叫 **ISSAbort::Abort** 而處於廢止狀態。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [ISSAbort &#40;OLE DB&#41;](https://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
