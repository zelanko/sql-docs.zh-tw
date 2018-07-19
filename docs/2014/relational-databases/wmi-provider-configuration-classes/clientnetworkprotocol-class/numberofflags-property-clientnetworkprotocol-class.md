---
title: NumberOfFlags 屬性 （ClientNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NumberOfFlags Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 10a3ca3269b07206ef9d67f28de4e490e77140b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256100"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 屬性 (ClientNetworkProtocol 類別)
  取得指定的用戶端網路通訊協定所需的旗標選項數[SetOrderValue 方法 （ClientNetworkProtocol 類別）](clientnetworkprotocol-class.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件，表示所使用的網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定 `Uint32` 屬性所參考之用戶端網路通訊協定所需旗標選項數的 `OrderValue` 值。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
