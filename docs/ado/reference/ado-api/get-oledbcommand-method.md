---
title: get_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
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
ms.openlocfilehash: e7b2668c3693078c7027b26fa61df73b81161970
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979350"
---
# <a name="getoledbcommand-method"></a>get_OLEDBCommand 方法
傳回基礎 OLE DB 命令，先傳播至 OLE DB 命令的 ADO 命令上設定任何參數資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>參數  
 *ppOLEDBCommand*  
 [out]將在其中寫入基礎 OLE DB 命令的 IUnknown 指標的指標位置指標。  
  
## <a name="applies-to"></a>適用於  
 [IADOCommandConstruction](http://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
