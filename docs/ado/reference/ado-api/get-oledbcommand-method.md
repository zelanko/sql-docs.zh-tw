---
title: get_OLEDBCommand 方法 |Microsoft 文件
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
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79990576ad2fbd9d6707aaa9a704c75e65e66a58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getoledbcommand-method"></a>get_OLEDBCommand 方法
傳回基礎 OLE DB 命令，先傳播至 OLE DB 命令 ADO 命令上設定任何參數資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *ppOLEDBCommand*  
 [out]寫入基礎 OLE DB 命令的 IUnknown 指標的指標位置指標。  
  
## <a name="applies-to"></a>適用於  
 [IADOCommandConstruction](http://msdn.microsoft.com/en-us/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
