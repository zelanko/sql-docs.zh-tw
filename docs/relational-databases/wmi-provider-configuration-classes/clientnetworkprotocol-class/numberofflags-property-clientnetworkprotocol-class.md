---
description: NumberOfFlags 屬性 (ClientNetworkProtocol 類別)
title: 'NumberOfFlags 屬性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 39d7143082e4d146f7c9c0d4c78e12ddfdecd579
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418892"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得 SetOrderValue 方法所指定之用戶端網路通訊協定所需的旗標選項數目 [ (ClientNetworkProtocol 類別) ](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，指定**OrderValue**屬性所參考的用戶端網路通訊協定所需的旗標選項數。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
