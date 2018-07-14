---
title: PropertyIdx 屬性 （ClientNetworkProtocolProperty 類別） |Microsoft Docs
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
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 331827dfd16ed941d903b5e877cb9c31b7ccc621
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37186185"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 屬性 (ClientNetworkProtocolProperty 類別)
  取得或設定屬性的索引值所參考的屬性陣列中[Properties 屬性 （ClientNetworkProtocol 類別）](../clientnetworkprotocol-class/clientnetworkprotocol-class.md)的[ClientNetworkProtocol 類別](../clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ClientNetworkProtocolProperty 類別](clientnetworkprotocolproperty-class.md)物件，表示屬性所使用之網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定目前屬性之陣列索引值的 `uint32` 值。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
