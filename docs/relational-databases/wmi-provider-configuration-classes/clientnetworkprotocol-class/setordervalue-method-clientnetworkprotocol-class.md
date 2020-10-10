---
description: SetOrderValue 方法 (ClientNetworkProtocol 類別)
title: 'SetOrderValue 方法 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1496143b862037ae8a4d0593ac3cc412dfd0b56e
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889158"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  從用戶端通訊協定清單中選取指定之順序值的通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*OrderValue*|設定順序值的 u**int32** 值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [用戶端通訊協定屬性 (順序索引標籤)](../../../tools/configuration-manager/client-protocols-properties-order-tab.md)  
  
