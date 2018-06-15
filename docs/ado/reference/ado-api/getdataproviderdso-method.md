---
title: GetDataProviderDSO 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40cf12ab80faf3c32da98c1fb97b7ec7d9ca373f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278817"
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
 這個方法就不 addref 介面指標。 如果呼叫端計劃將指標，呼叫端必須執行必要的 addref 和 release。  
  
## <a name="applies-to"></a>適用對象  
 [IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
