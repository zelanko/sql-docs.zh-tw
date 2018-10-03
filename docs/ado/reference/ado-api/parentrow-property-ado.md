---
title: ParentRow 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ea31baf4b215a6a516c13b438b526b8e9d8b612
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606576"
---
# <a name="parentrow-property-ado"></a>ParentRow 屬性 (ADO)
設定 OLE DB 的容器**資料列**物件上**ADORecordConstruction**物件，使資料列的父代變成 ADO**記錄**物件。  
  
 唯寫。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>參數  
 *pParent*  
 資料列的容器。  
  
## <a name="return-values"></a>傳回值  
 此屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
