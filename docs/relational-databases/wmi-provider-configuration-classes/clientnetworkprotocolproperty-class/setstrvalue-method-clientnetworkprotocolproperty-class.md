---
title: SetStrValue 方法（ClientNetworkProtocolProperty）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStrValue Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4748b618d4811d5069a7be51bc30619597d97f08
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888891"
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>SetStrValue 方法 (ClientNetworkProtocolProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定[PropertyIdx 屬性（ClientNetworkProtocolProperty 類別）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值所參考之目前屬性的字串值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ClientNetworkProtocolProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)物件，代表用戶端所使用之網路通訊協定的屬性 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|*StrValue*|指定目前屬性之新值的字串值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
