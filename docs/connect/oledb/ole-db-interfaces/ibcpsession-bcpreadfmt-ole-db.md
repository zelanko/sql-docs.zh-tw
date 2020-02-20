---
title: IBCPSession::BCPReadFmt (OLE DB) | Microsoft Docs
description: 使用 IBCPSession::BCPReadFmt 從格式檔案讀取資料 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 97274315275f11e77c458827740f44906a524ed9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015506"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  從格式檔案中讀取每個資料行的格式資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 **BCPReadFmt** 方法是用來讀取格式檔案中的資料 (格式檔案會指定資料檔中的資料格式)。 這個方法能夠偵測格式檔案的正確版本。 它可以自動偵測格式檔案為 xml 還是舊樣式的文字格式，並適當地產生行為。 OLE DB Driver for SQL Server BCP 支援的格式檔案版本為 6.0 版或更新版本。  
  
 當 **BCPReadFmt** 方法讀取格式值以後，它會適當地呼叫 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 方法。 使用者不需要剖析格式檔案，也不需要進行這些呼叫。  
  
 若要儲存格式檔案，請呼叫 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 方法。 **BCPReadFmt** 方法的呼叫可以參考已儲存的格式。 另外，大量複製公用程式 (**bcp**) 可以將使用者定義的資料格式儲存在由 **BCPReadFmt** 方法參考的檔案中。  
  
 [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 之 *eOption* 參數的 **BCP_OPTION_DELAYREADFMT** 值會修改 IBCPSession::BCPReadFmt 的行為。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
