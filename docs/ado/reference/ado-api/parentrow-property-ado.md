---
title: ParentRow 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: a81eb6ee58d942547a159728b9c3edf9a30f1ece
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917677"
---
# <a name="parentrow-property-ado"></a>ParentRow 屬性 (ADO)
設定**ADORecordConstruction**物件上 OLE DB **row**物件的容器，以便將資料列的父系轉換成 ADO **Record**物件。  
  
 唯寫。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>參數  
 *pParent*  
 資料列的容器。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
