---
description: Stream 屬性
title: 資料流程屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1903644370172e716de78bc49a68af03a742c125
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988509"
---
# <a name="stream-property"></a>Stream 屬性
從**ADOStreamConstruction**物件取得或設定 OLE DB**資料流程**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>參數  
 *ppStream*  
 OLE DB **資料流程** 物件的指標。  
  
 *pStream*  
 OLE DB **資料流程** 物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準的 HRESULT 值。 這包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADOStreamConstruction 介面](./adostreamconstruction-interface.md)