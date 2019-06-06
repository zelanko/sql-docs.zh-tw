---
title: InvokeService (RDS) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: d7d0c205b5045f4cd743776894f62fbc4f0750cc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712650"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
傳回要求的介面指標上能力更強的版本的物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>參數  
 *riid*  
  
 [in]所要求的介面識別碼。  
  
 *punkNotSoFunctionalInterface*  
  
 [in]效能較差的來源物件。  
  
 *ppunkMoreFunctionalInterface*  
  
 [out]接收要求中的介面指標的指標變數的位址*riid*。 在成功傳回時， *ppunkMoreFunctionalInterface*參數包含的物件要求的介面指標。 如果物件不支援指定的介面*riid*， *ppunkMoreFunctionalInterface*設為 NULL。  
  
## <a name="return-value"></a>傳回值  
 HRESULT 值，指出如果在呼叫**InvokeService**方法是否成功。  
  
## <a name="remarks"></a>備註  
 RDS 資料指標引擎實作**InvokeService**接受輸入的資料列集 （或多個結果的物件），填入資料指標引擎，從輸入資料列集，然後將指標傳回本身。  
  
## <a name="applies-to"></a>適用於  
 [IRDSService 介面 (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [RDS 方法](../../../ado/reference/rds-api/rds-methods.md)


