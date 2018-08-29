---
title: Bcpexec (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e72a25d3c7fd6416400bf21ac252363fe864fdf
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079117"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  執行大量複製作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>備註  
 根據與 [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法搭配使用之 *eDirection* 參數的值，**BCPExec** 方法會將資料從使用者檔案複製到資料庫資料表，反之亦然。  
  
 呼叫 **BCPExec** 之前，請使用有效的使用者檔案名稱來呼叫 **BCPInit** 方法。 無法執行這項操作時，會發生錯誤。 唯一的例外狀況是針對大量複製輸出作業使用查詢。 在該情況下，請針對 **BCPInit** 方法中的資料表名稱指定 NULL，然後使用 BCP_OPTION_HINTS 選項來指定查詢。  
  
 **BCPExec** 方法是唯一可能持續任何時間長度的大量複製方法。 因此，它是唯一支援非同步模式的大量複製方法。 若要使用非同步模式，請在呼叫 **BCPExec** 方法之前將提供者特定的工作階段屬性 SSPROP_ASYNCH_BULKCOPY 設定為 VARIANT_TRUE。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。 若要測試是否完成，請使用相同的參數來呼叫 **BCPExec** 方法。 如果大量複製尚未完成，**BCPExec** 方法就會傳回 DB_S_ASYNCHRONOUS。 它也會在 *pRowsCopied* 引數中傳回已經傳送至伺服器或從伺服器接收之資料列數目的狀態計數。 到達批次的結尾之前，不會認可傳送至伺服器的資料列。  
  
## <a name="arguments"></a>引數  
 *pRowsCopied*[out]  
 DWORD 的指標。 **BCPExec** 方法會將成功複製的資料列數目填入 DWORD。 如果 *pRowsCopied* 引數設定為 NULL，**BCPExec** 方法就會忽略此引數。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 **BCPInit** 方法。 此外，如果已經透過使用 BCP_OPTION_ABORT 選項來中止此作業，之後再呼叫 **BCPExec** 方法，也會發生這種情況。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 DB_S_ENDOFROWSET  
 大量複製作業已完成，而且所有資料傳送都已完成。  
  
 DB_S_ASYNCHRONOUS  
 已經複製目前的資料列批次。 請再次呼叫 **BCPExec** 方法來傳送下一個批次。  
  
 DB_S_ERRORSOCCURRED  
 在大量複製作業期間發生了錯誤，而且可能尚未複製某些資料列。 錯誤數目仍然少於允許的最大錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
