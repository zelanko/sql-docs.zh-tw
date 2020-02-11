---
title: InvokeService （RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86ebb27ebdc5de5a045304afe45cd8653e491827
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963867"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
在物件的支援版本上，傳回所要求介面的指標。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>參數  
 *riid*  
  
 在所要求之介面的識別碼。  
  
 *punkNotSoFunctionalInterface*  
  
 在較不支援的來源物件。  
  
 *ppunkMoreFunctionalInterface*  
  
 脫銷指標變數的位址，其會接收在*riid*中要求的介面指標。 成功傳回時， *ppunkMoreFunctionalInterface*參數會包含所要求的介面指標給物件。 如果物件不支援*riid*中指定的介面， *ppunkMoreFunctionalInterface*會設定為 Null。  
  
## <a name="return-value"></a>傳回值  
 HRESULT 值，指出**InvokeService**方法的呼叫是否成功。  
  
## <a name="remarks"></a>備註  
 **InvokeService**的 RDS 資料指標引擎執行會接受輸入資料列集（或多個結果物件）、填入輸入資料列集的資料指標引擎，然後在其本身上傳回指標。  
  
## <a name="applies-to"></a>套用至  
 [IRDSService 介面 (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [RDS 方法](../../../ado/reference/rds-api/rds-methods.md)


