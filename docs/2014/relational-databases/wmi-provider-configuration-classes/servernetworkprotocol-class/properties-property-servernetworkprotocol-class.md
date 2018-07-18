---
title: Properties 屬性 （ServerNetworkProtocol 類別） |Microsoft Docs
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
- Properties Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cf3384908284cb25a59c35451706b0e3e535e345
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157869"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Properties 屬性 (ServerNetworkProtocol 類別)
  取得與伺服器網路通訊協定相關聯的屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ServerNetworkProtocol 類別](servernetworkprotocol-class.md)物件，表示執行個體所使用的網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 陣列[ServerNetworkProtocolProperty 類別](../servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md)代表伺服器網路通訊協定所支援之屬性的物件。  
  
## <a name="remarks"></a>備註  
  
