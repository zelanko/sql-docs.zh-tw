---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f7b2437a8a1a46b84f011eb631887d39f7c96eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031415"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  將每個資料行的格式資訊寫入格式檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 格式檔案會指定大量複製所建立之資料檔的資料格式。 呼叫[ibcpsession:: Bcpcolumns](ibcpsession-bcpcolumns-ole-db.md)和[ibcpsession:: Bcpcolfmt](ibcpsession-bcpcolfmt-ole-db.md)方法定義的資料檔案格式。 **BCPWriteFmt**方法會將此定義儲存在 pwszFormatFile 引數參考的檔案中。  
  
 **BCPWriteFmt**方法可以將格式檔案儲存在 xml 或文字格式。 這必須使用 BCP_OPTION_XML 控制選項，以表示[ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md)方法。  
  
 若要載入已儲存的格式檔案，請使用[ibcpsession:: Bcpreadfmt](ibcpsession-bcpreadfmt-ole-db.md)方法。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤。詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， [ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)方法不會呼叫這個方法之前呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)  
  
  