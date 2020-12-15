---
description: 'IBCPSession：： BCPWriteFmt (Native Client OLE DB 提供者) '
title: IBCPSession：： BCPWriteFmt (Native Client OLE DB provider) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6f69d1d82101d96725e79f65fcc6667986ecb81
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484950"
---
# <a name="ibcpsessionbcpwritefmt-native-client-ole-db-provider"></a>IBCPSession：： BCPWriteFmt (Native Client OLE DB 提供者) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將每個資料行的格式資訊寫入格式檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>備註  
 格式檔案會指定大量複製所建立之資料檔的資料格式。 [IBCPSession::BCPColumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 方法的呼叫會定義資料檔案的格式。 **BCPWriteFmt** 方法會將此定義儲存在 pwszFormatFile 引數參考的檔案中。  
  
 **BCPWriteFmt** 方法可以用 xml 或文字格式儲存格式檔案。 這必須搭配 [IBCPSession::BCPControl](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 方法使用 BCP_OPTION_XML 控制選項指示。  
  
 若要載入已儲存的格式檔案，請使用 [IBCPSession::BCPReadFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 方法。  
  
## <a name="arguments"></a>引數  
 *pwszFormatFile*[in]  
 包含資料檔案式值之檔案的路徑和檔案名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](isqlservererrorinfo-geterrorinfo-ole-db.md) 介面。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
