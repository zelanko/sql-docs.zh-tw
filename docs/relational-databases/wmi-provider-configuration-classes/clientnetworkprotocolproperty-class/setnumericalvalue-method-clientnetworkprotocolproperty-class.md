---
description: SetNumericalValue 方法 (ClientNetworkProtocolProperty 類別)
title: 'SetNumericalValue 方法 (ClientNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumericalValue Method (ClientNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: d4d6df52-9e68-4003-9e28-ece6716ba7f1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0503bf1ea27981f986e20dcf1134df4f6dab912d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537215"
---
# <a name="setnumericalvalue-method-clientnetworkprotocolproperty-class"></a>SetNumericalValue 方法 (ClientNetworkProtocolProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定 PropertyIdx 屬性所參考之目前屬性的數值， [ (ClientNetworkProtocolProperty 類別) ](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetNumericalValue [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ClientNetworkProtocolProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)物件，代表 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 用戶端所使用之網路通訊協定的屬性 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*value*|指定所參考屬性之數值的 **uint32** 值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
