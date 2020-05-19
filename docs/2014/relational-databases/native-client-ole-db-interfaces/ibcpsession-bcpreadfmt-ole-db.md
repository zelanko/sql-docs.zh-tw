---
title: IBCPSession::BCPReadFmt (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54cfcdb87e8292f4588360e5a6b8c77f410a1fc9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82695408"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  從格式檔案中讀取每個資料行的格式資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 **BCPReadFmt** 方法是用來讀取格式檔案中的資料 (格式檔案會指定資料檔中的資料格式)。 這個方法能夠偵測格式檔案的正確版本。 它可以自動偵測格式檔案為 xml 還是舊樣式的文字格式，並適當地產生行為。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者 BCP 支援的格式檔案版本是6.0 或更新版本。  
  
 當 **BCPReadFmt** 方法讀取格式值以後，它會適當地呼叫 [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 方法。 使用者不需要剖析格式檔案，也不需要進行這些呼叫。  
  
 若要儲存格式檔案，請呼叫 [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) 方法。 **BCPReadFmt** 方法的呼叫可以參考已儲存的格式。 另外，大量複製公用程式 (**bcp**) 可以將使用者定義的資料格式儲存在由 **BCPReadFmt** 方法參考的檔案中。  
  
 `BCP_OPTION_DELAYREADFMT` [IBCPSession：： BCPControl](ibcpsession-bcpcontrol-ole-db.md)的*eOption*參數值會修改 IBCPSession：： BCPReadFmt 的行為。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 介面。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)  
  
  
