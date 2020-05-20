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
author: rothja
ms.author: jroth
ms.openlocfilehash: 55272fdbcd0aacfc8e98cb4e38ae19270b3b461a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760044"
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
 脫銷 指標的指標，會傳回基礎 OLE DB 資料來源物件的 IUnknown。  
  
## <a name="remarks"></a>備註  
 這個方法不會 addref 介面指標。 如果呼叫端計畫保留指標，則呼叫端必須執行必要的 addref 和發行。  
  
## <a name="applies-to"></a>適用於  
 [IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
