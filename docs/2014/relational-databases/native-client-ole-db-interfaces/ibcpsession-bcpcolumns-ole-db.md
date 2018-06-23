---
title: 'Ibcpsession:: Bcpcolumns (OLE DB) |Microsoft 文件'
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
- IBCPSession::BCPColumns (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f337a918f1281073a70422db307f2698742d5f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022612"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
  設定要繫結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中之資料行的欄位數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPColumns(   
DBCOUNTITEMnColumns);  
```  
  
## <a name="remarks"></a>備註  
 它會在內部呼叫[ibcpsession:: Bcpcolfmt](ibcpsession-bcpcolfmt-ole-db.md)設定欄位資料的預設值。 這些預設值從提供者，在內部擷取透過指定資料表名稱時，SQL Server 資料行資訊取得[ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)。  
  
> [!NOTE]  
>  這個方法後，才可以呼叫**BCPInit**已使用有效的檔案名稱呼叫。  
  
 只有打算使用與預設值不同的使用者檔案格式時，才可以呼叫此方法。 如需預設使用者檔案格式描述的詳細資訊，請參閱**BCPInit**方法。  
  
 在呼叫**BCPColumns**方法，您必須呼叫**BCPColFmt**以完整定義自訂的檔案格式的使用者檔案中的每個資料行的方法。  
  
## <a name="arguments"></a>引數  
 *nColumns*[in]  
 使用者檔案中的欄位總數。 即使您準備要從使用者檔案的 SQL server 的大量複製資料的資料表，並不想複製使用者檔案中的所有欄位，您仍然必須設定*nColumns*使用者檔案欄位的總數目的引數。 然後可以透過指定略過的欄位**BCPColFmt**。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤。詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， **BCPInit**方法不會呼叫這個方法之前呼叫。 針對大量複製作業呼叫此方法超過一次時，也會發生這個狀況。  
  
 E_OUTOFMEMORY  
 記憶體不足錯誤  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)  
  
  