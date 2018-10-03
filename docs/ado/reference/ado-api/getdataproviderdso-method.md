---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c7d864d61d2782955a52ce6e20a7025379cc946
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47744066"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 方法
從 Shape 提供者擷取基礎 OLE DB 資料來源物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>參數  
 *ppDataProviderDSOIUnknown*  
 [out] 傳回基礎 OLE DB 資料來源物件的 IUnknown 指標的指標。  
  
## <a name="remarks"></a>備註  
 這個方法就不 addref 的介面指標。 如果呼叫端，計劃將指標，呼叫端必須執行必要的 addref 和 release。  
  
## <a name="applies-to"></a>適用對象  
 [IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
