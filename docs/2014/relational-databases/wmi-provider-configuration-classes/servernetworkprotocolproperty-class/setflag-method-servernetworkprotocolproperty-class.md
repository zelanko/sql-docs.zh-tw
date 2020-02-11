---
title: SetFlag 方法（ServerNetworkProtocolProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 95288931-8eb1-4477-ad80-619cf7073e61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 95682cc34f67a0d65f62afdc52ec09c5209e3ba4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62642680"
---
# <a name="setflag-method-servernetworkprotocolproperty-class"></a>SetFlag 方法 (ServerNetworkProtocolProperty 類別)
  設定參考之屬性的旗標。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetFlag(  
BoolValue  
)  
  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 [ServerNetworkProtocolProperty 類別] ServerNetworkProtocolProperty-class.md）物件，代表實例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上網路通訊協定的屬性。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*BoolValue*|指定旗標之新值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 
  `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
