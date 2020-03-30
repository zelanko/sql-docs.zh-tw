---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) | Microsoft Docs
description: ISQLServerErrorInfo::GetErrorInfo (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 54e9c71ca21647004ea3899306dcb15689dcc3d0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015445"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  傳回包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤詳細資料之 OLE DB Driver for SQL Server SSERRORINFO 結構的指標。  
  
 OLE DB Driver for SQL Server 定義 **ISQLServerErrorInfo** 錯誤介面。 此介面會傳回來自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤的詳細資料，包括其嚴重性和狀態。  

  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>引數  
 *ppSSErrorInfo*[out]  
 SSERRORINFO 結構的指標。 如果方法失敗，或者沒有與錯誤建立關聯的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資訊，提供者就不會配置任何記憶體，也無法確保輸出時，*ppSSErrorInfo* 引數為 Null 指標。  
  
 *ppErrorStrings*[out]  
 Unicode 字元字串指標的指標。 如果方法失敗，或者沒有與錯誤建立關聯的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資訊，提供者就不會配置任何記憶體，也無法確保輸出時，*ppErrorStrings* 引數為 Null 指標。 使用 *IMalloc::Free* 方法釋放 **ppErrorStrings** 引數時，會釋放傳回之 SSERRORINFO 結構的三個個別字串成員，因為有在區塊中配置記憶體。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_INVALIDARG  
 *ppSSErrorInfo* 或 *ppErrorStrings* 引數為 NULL。  
  
 E_OUTOFMEMORY  
 OLE DB Driver for SQL Server 無法配置足夠的記憶體來完成要求。  
  
## <a name="remarks"></a>備註  
 OLE DB Driver for SQL Server 會針對透過取用者傳遞之指標所傳回的 SSERRORINFO 和 OLECHAR 字串配置記憶體。 當取用者不再需要存取錯誤資料時，必須使用 **IMalloc::Free** 方法來取消配置這個記憶體。  
  
 SSERRORINFO 結構定義如下：  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|member|描述|  
|------------|-----------------|  
|*pwszMessage*|來自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的錯誤訊息。 此訊息會透過 **IErrorInfo::GetDescription** 方法傳回。|  
|*pwszServer*|發生錯誤之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|*pwszProcedure*|如果在預存程序中發生錯誤，則是產生錯誤之預存程序的名稱，否則為空字串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤號碼。 此錯誤號碼與 *ISQLErrorInfo::GetSQLInfo* 方法之 **plNativeError** 參數中所傳回的錯誤號碼相同。|  
|*bState*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤的狀態。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤的嚴重性。|  
|*wLineNumber*|在適用時，這是產生錯誤訊息之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預存程序的行號。 如果不包含任何程序，預設值為 1。|  
  
 結構中的指標會參考 *ppErrorStrings* 引數所傳回之字串中的地址。  
  
## <a name="see-also"></a>另請參閱  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
