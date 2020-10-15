---
title: IBCPSession::BCPWriteFmt (OLE DB 驅動程式) | Microsoft Docs
description: 使用 IBCPSession::BCPWriteFmt 方法將格式檔案儲存為 xml 或文字格式 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c088997b86fa8f0a5bd87d6497f9945c3ca2da8d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081387"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  將每個資料行的格式資訊寫入格式檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 格式檔案會指定大量複製所建立之資料檔的資料格式。 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 方法的呼叫會定義資料檔案的格式。 **BCPWriteFmt** 方法會將此定義儲存在 pwszFormatFile 引數參考的檔案中。  
  
 **BCPWriteFmt** 方法可以用 xml 或文字格式儲存格式檔案。 這必須搭配 [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 方法使用 BCP_OPTION_XML 控制選項指示。  
  
 若要載入已儲存的格式檔案，請使用 [IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 方法。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md) 介面。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md) 
  
