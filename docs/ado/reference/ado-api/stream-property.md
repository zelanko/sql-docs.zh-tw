---
title: 資料流程屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58bbbc299f13c0d876807476136cede76894bbb8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916692"
---
# <a name="stream-property"></a>Stream 屬性
取得或設定**ADOStreamConstruction**物件上/的 OLE DB**資料流程**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>參數  
 *ppStream*  
 OLE DB**資料流程**物件的指標。  
  
 *pStream*  
 OLE DB**資料流程**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準的 HRESULT 值。 這包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADOStreamConstruction 介面](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
