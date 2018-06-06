---
title: put_OLEDBCommand 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04efb030e38f6afe212aca5591c7098b072e517b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="putoledbcommand-method"></a>put_OLEDBCommand 方法
這個方法會執行任何作業並一律傳回 S_OK。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *pOLEDBCommand*  
 [in]OLE DB 命令物件的指標。  
  
## <a name="applies-to"></a>適用於  
 [IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)
