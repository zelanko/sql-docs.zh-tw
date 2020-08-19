---
description: get_OLEDBCommand 方法
title: get_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 562b10fa67b04926e512833248c99ecb7b55a1fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443600"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand 方法
傳回基礎 OLE DB 命令，先將 ADO 命令上設定的任何參數資訊傳播至 OLE DB 命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *ppOLEDBCommand*  
 擴展指標位置的指標，其中將會寫入基礎 OLE DB 命令的 IUnknown 指標。  
  
## <a name="applies-to"></a>套用至  
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
