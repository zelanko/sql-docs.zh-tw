---
title: Bcpexec (OLE DB) |Microsoft 文件
description: IBCPSession::BCPExec (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPExec method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9cd489ba5fb5057d1f1b62ad3122b791ee135f57
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  執行大量複製作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>備註  
 **BCPExec**方法將資料從使用者檔案至資料庫資料表，或反之亦然，複製的值而定*eDirection*參數搭配[ibcpsession:: Bcpinit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)方法。  
  
 然後再呼叫**BCPExec**，呼叫**BCPInit**具有有效的使用者檔案名稱的方法。 無法執行這項操作時，會發生錯誤。 唯一的例外狀況是針對大量複製輸出作業使用查詢。 在此情況下中的資料表名稱指定 NULL **BCPInit**方法，然後指定 使用 BCP_OPTION_HINTS 選項的查詢。  
  
 **BCPExec**方法是唯一大量複製方法很可能是任何長度的時間。 因此，它是唯一支援非同步模式的大量複製方法。 若要使用非同步模式中，設定提供者特定的工作階段屬性 ssprop_asynch_bulkcopy 設定為 VARIANT_TRUE 會在呼叫之前**BCPExec**方法。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。 若要測試是否完成，呼叫**BCPExec**具有相同參數的方法。 如果大量複製尚未完成， **BCPExec**方法會傳回 DB_S_ASYNCHRONOUS。 它也會傳回在*pRowsCopied*引數傳送至或從伺服器收到的資料列數目的狀態計數。 到達批次的結尾之前，不會認可傳送至伺服器的資料列。  
  
## <a name="arguments"></a>引數  
 *pRowsCopied*[out]  
 DWORD 的指標。 **BCPExec**方法已成功複製的資料列數目填入 DWORD。 如果*pRowsCopied*引數設定為 NULL 時，會忽略它**BCPExec**方法。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤。詳細資訊，請使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， **BCPInit**方法不會呼叫這個方法之前呼叫。 如果作業已中止，透過使用 BCP_OPTION_ABORT 選項，也會發生與**BCPExec**方法之後呼叫。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
 DB_S_ENDOFROWSET  
 大量複製作業已完成，而且所有資料傳送都已完成。  
  
 DB_S_ASYNCHRONOUS  
 已經複製目前的資料列批次。 呼叫**BCPExec**再次傳送下一個批次的方法。  
  
 DB_S_ERRORSOCCURRED  
 在大量複製作業期間發生了錯誤，而且可能尚未複製某些資料列。 錯誤數目仍然少於允許的最大錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
