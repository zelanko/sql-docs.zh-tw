---
title: NumberOfFlags 屬性（ClientNetworkProtocol）
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
ms.openlocfilehash: 48f81c86a823d75d501187ef953930ec92083d27
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659120"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得[SetOrderValue 方法（ClientNetworkProtocol 類別）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)所指定之用戶端網路通訊協定所需的旗標選項數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，指定**OrderValue**屬性所參考之用戶端網路通訊協定所需的旗標選項數目。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
