---
description: InvokeService (RDS)
title: InvokeService (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d3dc0ca3744f715f080e5e34a9d4cd5e88bc8b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724489"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
在更強大的物件版本上，將指標傳回至要求的介面。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至  [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>參數  
 *riid*  
  
 在所要求之介面的識別碼。  
  
 *punkNotSoFunctionalInterface*  
  
 在功能較少的來源物件。  
  
 *ppunkMoreFunctionalInterface*  
  
 擴展指標變數的位址，此變數會接收在 *riid*中要求的介面指標。 在成功傳回時， *ppunkMoreFunctionalInterface* 參數會包含要求的物件介面指標。 如果物件不支援在 *riid*中指定的介面， *ppunkMoreFunctionalInterface* 會設為 Null。  
  
## <a name="return-value"></a>傳回值  
 HRESULT 值，指出對 **InvokeService** 方法的呼叫是否成功。  
  
## <a name="remarks"></a>備註  
 **InvokeService**的 RDS 資料指標引擎實採用輸入資料列集 (或多個結果物件) 、從輸入資料列集填入資料指標引擎，然後將指標傳回本身。  
  
## <a name="applies-to"></a>套用至  
 [IRDSService 介面 (RDS)](./irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [RDS 方法](./rds-methods.md)