---
title: 'Ibcpsession:: Bcpcolumns (OLE DB) |Microsoft Docs'
description: IBCPSession::BCPColumns (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ef5e483f32582a5a0f7952070ddf0c5becce6382
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672226"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  設定要繫結至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中之資料行的欄位數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Remarks  
 它會在內部呼叫 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 來設定欄位資料的預設值。 這些預設值會從 SQL Server 資料行資訊取得，提供者會在透過 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 指定資料表名稱時，在內部擷取這項資訊。  
  
> [!NOTE]  
>  只有在已使用有效的檔案名稱呼叫 **BCPInit** 後，才可以呼叫這個方法。  
  
 只有打算使用與預設值不同的使用者檔案格式時，才可以呼叫此方法。 如需預設使用者檔案格式之描述的詳細資訊，請參閱 **BCPInit** 方法。  
  
 在呼叫 **BCPColumns** 方法之後，您必須針對使用者檔案中的每個資料行呼叫 **BCPColFmt** 方法，以完整定義自訂的檔案格式。  
  
## <a name="arguments"></a>引數  
 *nColumns*[in]  
 使用者檔案中的欄位總數。 即使您準備要將資料從使用者檔案大量複製到 SQL Server 資料表，而不想複製使用者檔案中的所有欄位，也仍必須將 *nColumns* 引數設定為使用者檔案欄位的總數。 接著，系統可以透過 **BCPColFmt** 指定略過的欄位。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 **BCPInit** 方法。 針對大量複製作業呼叫此方法超過一次時，也會發生這個狀況。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
