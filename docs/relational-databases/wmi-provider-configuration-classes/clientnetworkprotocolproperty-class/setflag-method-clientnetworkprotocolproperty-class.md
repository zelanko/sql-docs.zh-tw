---
description: SetFlag 方法 (ClientNetworkProtocolProperty 類別)
title: 'SetFlag 方法 (ClientNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetFlag Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 69cd62178a35ea88c9a2d76bff14cb6b4405a061
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537201"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>SetFlag 方法 (ClientNetworkProtocolProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定 PropertyIdx 屬性所參考之目前屬性的旗標 [ (ClientNetworkProtocolProperty 類別) ](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetFlag(BoolValue) [=]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ClientNetworkProtocolProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)物件，代表 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 用戶端所使用之網路通訊協定的屬性 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*BoolValue*|指定旗標之新值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
