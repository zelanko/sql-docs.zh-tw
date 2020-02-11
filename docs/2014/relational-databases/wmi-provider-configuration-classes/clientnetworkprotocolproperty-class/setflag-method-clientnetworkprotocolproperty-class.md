---
title: SetFlag 方法（ClientNetworkProtocolProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6c33eca0bf3281243aeee42ed89001cf9108d5d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245085"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>SetFlag 方法 (ClientNetworkProtocolProperty 類別)
  設定[PropertyIdx 屬性（ClientNetworkProtocolProperty 類別）](clientnetworkprotocolproperty-class.md)值所參考之目前屬性的旗標。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetFlag(  
BoolValue  
) [=]  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 [ClientNetworkProtocolProperty 類別](clientnetworkprotocolproperty-class.md)物件，代表[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端所使用之網路通訊協定的屬性。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*BoolValue*|指定旗標之新值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 
  `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
