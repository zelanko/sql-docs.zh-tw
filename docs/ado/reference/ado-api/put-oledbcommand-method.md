---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dc19da014bc0909e44180ff4176adf1902694b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278946"
---
# <a name="putoledbcommand-method"></a>put_OLEDBCommand 方法
這個方法會執行任何作業，而且一律會傳回 S_OK。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *pOLEDBCommand*  
 [in]OLE DB Command 物件的指標。  
  
## <a name="applies-to"></a>適用於  
 [IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)
