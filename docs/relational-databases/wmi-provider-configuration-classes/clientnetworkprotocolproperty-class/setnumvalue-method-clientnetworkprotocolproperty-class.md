---
description: SetNumValue 方法 (ClientNetworkProtocolProperty 類別)
title: 'SetNumValue 方法 (ClientNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumValue Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumValue method
ms.assetid: c292e2ae-6d0a-44ad-ba54-5b0bd705ef37
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c886de5179bbcbfdc81c08e0ac910d0c2272eb39
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537166"
---
# <a name="setnumvalue-method-clientnetworkprotocolproperty-class"></a>SetNumValue 方法 (ClientNetworkProtocolProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定 PropertyIdx 屬性所參考之目前屬性的數值， [ (ClientNetworkProtocolProperty 類別) ](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetNumValue [= value]  
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
  
  
