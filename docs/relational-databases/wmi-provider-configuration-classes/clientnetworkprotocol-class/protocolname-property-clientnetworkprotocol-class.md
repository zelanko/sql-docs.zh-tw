---
description: ProtocolName 屬性 (ClientNetworkProtocol 類別)
title: 'ProtocolName 屬性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1323d4c47555bfebb717ba1627e6b4fc7c22c94b
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888928"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)所指定之目前網路通訊協定的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 字串值，指定 [SetOrderValue 方法 (ClientNetworkProtocol 類別 ](./setordervalue-method-clientnetworkprotocol-class.md)所參考的目前用戶端網路通訊協定名稱) 。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
