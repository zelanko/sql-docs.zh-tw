---
title: "Ibcpsession:: Bcpreadfmt (OLE DB) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords: BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c22174eb0cca7cc653b5b0f65421720a59d442f3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  從格式檔案中讀取每個資料行的格式資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 **BCPReadFmt**方法，可用來從資料檔中指定的資料格式的格式檔案讀取資料。 這個方法能夠偵測格式檔案的正確版本。 它可以自動偵測格式檔案為 xml 還是舊樣式的文字格式，並適當地產生行為。 支援的格式檔案版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者 BCP 為 6.0 版或更新版本。  
  
 之後**BCPReadFmt**方法讀取格式值，它會適當地呼叫[ibcpsession:: Bcpcolumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)和[ibcpsession:: Bcpcolfmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)方法。 使用者不需要剖析格式檔案，也不需要進行這些呼叫。  
  
 若要儲存的格式檔案，請呼叫[ibcpsession:: Bcpwritefmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)方法。 呼叫**BCPReadFmt**方法可以參考已儲存的格式。 或者，大量複製公用程式 (**bcp**) 可以將使用者定義資料格式儲存在檔案可以參考的**BCPReadFmt**方法。  
  
 **BCP_OPTION_DELAYREADFMT**值*eOption*參數[ibcpsession:: Bcpcontrol](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)修改 ibcpsession:: Bcpreadfmt 的行為。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 提供者特定錯誤發生，詳細的資訊，請使用如[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)介面。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， [ibcpsession:: Bcpinit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)方法不會呼叫這個方法之前呼叫。  
  
## <a name="see-also"></a>請參閱＜  
 [IBCPSession &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
