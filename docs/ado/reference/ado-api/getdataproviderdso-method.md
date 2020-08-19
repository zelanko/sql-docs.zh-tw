---
description: GetDataProviderDSO 方法
title: GetDataProviderDSO 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a45d78960b8b6b1ba2534e39f080a6c94fc0655
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443570"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 方法
從圖形提供者抓取基礎 OLE DB 資料來源物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>參數  
 *ppDataProviderDSOIUnknown*  
 擴展 指標的指標，該指標會傳回基礎 OLE DB 資料來源物件的 IUnknown。  
  
## <a name="remarks"></a>備註  
 這個方法不會 addref 介面指標。 如果呼叫端計畫要保留指標，則呼叫端必須進行必要的 addref 和發行。  
  
## <a name="applies-to"></a>適用於  
 [IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
