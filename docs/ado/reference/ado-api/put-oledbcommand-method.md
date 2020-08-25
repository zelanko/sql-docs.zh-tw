---
description: put_OLEDBCommand 方法
title: put_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: e386485f5e430a1bda50aa0d2059aeca90525af2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772767"
---
# <a name="put_oledbcommand-method"></a>put_OLEDBCommand 方法
這個方法不會執行任何作業，而且一律會傳回 S_OK。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *pOLEDBCommand*  
 在OLE DB 命令物件的指標。  
  
## <a name="applies-to"></a>套用至  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))