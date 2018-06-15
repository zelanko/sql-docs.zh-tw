---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) |Microsoft 文件'
description: '使用 ibcpsession:: Bcpwritefmt 儲存格式檔案以 xml 或文字格式 (OLE DB)'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2c2e879ded8e42a29c4dfe14226b27e252c09c42
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35304977"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  將每個資料行的格式資訊寫入格式檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 格式檔案會指定大量複製所建立之資料檔的資料格式。 呼叫[ibcpsession:: Bcpcolumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)和[ibcpsession:: Bcpcolfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)方法定義的資料檔案格式。 **BCPWriteFmt**方法會將此定義儲存在 pwszFormatFile 引數參考的檔案中。  
  
 **BCPWriteFmt**方法可以將格式檔案儲存在 xml 或文字格式。 這必須使用 BCP_OPTION_XML 控制選項，以表示[ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)方法。  
  
 若要載入已儲存的格式檔案，請使用[ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)方法。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤。詳細資訊，請使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)介面。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， [ibcpsession:: Bcpinit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)方法不會呼叫這個方法之前呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md) 
  
  
