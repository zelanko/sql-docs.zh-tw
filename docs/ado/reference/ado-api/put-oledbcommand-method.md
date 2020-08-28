---
description: put_OLEDBCommand 方法
title: put_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5239a1b1924cb767d0425b2a6c686fc15607a08a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989939"
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