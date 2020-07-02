---
title: PropertyNumVal 屬性（ClientNetworkProtocolProperty）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyNumVal Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyNumVal property
ms.assetid: 12b02d97-702b-434f-baf6-e49a6b2cd4de
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b0bf763d677743dbcf8a2dde55b5abdb238559e8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722799"
---
# <a name="propertynumval-property-clientnetworkprotocolproperty-class"></a>PropertyNumVal 屬性 (ClientNetworkProtocolProperty 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  取得[PropertyIdx 屬性（ClientNetworkProtocolProperty 類別）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值所參考之目前屬性的數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.PropertyNumVal [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ClientNetworkProtocolProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)物件，代表用戶端所使用之網路通訊協定的屬性 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 U**int32**值，指定目前屬性的數值。  
  
## <a name="remarks"></a>備註  
  
