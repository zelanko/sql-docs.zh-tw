---
title: IBCPSession::BCPColumns (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColumns (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7108760ebdb5e7e3e6367b801b07d4f8140a62d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63238739"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
  設定要繫結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中之資料行的欄位數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPColumns(   
DBCOUNTITEMnColumns);  
```  
  
## <a name="remarks"></a>備註  
 它會在內部呼叫 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 來設定欄位資料的預設值。 這些預設值會從 SQL Server 資料行資訊取得，提供者會在透過 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 指定資料表名稱時，在內部擷取這項資訊。  
  
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
 發生提供者特定的錯誤;如需詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 **BCPInit** 方法。 針對大量複製作業呼叫此方法超過一次時，也會發生這個狀況。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)  
  
  
