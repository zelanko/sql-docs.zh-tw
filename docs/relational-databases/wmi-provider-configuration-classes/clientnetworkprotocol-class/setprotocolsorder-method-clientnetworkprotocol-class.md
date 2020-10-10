---
description: SetProtocolsOrder 方法 (ClientNetworkProtocol 類別)
title: 'SetProtocolsOrder 方法 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetProtocolsOrder Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetProtocolsOrder method
ms.assetid: b86d98b9-aae4-4e74-b4da-1ec984d5c8b4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 047a078e93a4683647f65e5cdc702d89199a6123
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889045"
---
# <a name="setprotocolsorder-method-clientnetworkprotocol-class"></a>SetProtocolsOrder 方法 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  變更通訊協定清單的順序。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetProtocolsOrder(ProtocolOrderList)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*ProtocolOrderList*|以新的順序列出用戶端網路通訊協定的 string[] 陣列。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](../../../database-engine/configure-windows/configure-client-protocols.md)   
 [設定用戶端網路通訊協定和網路程式庫](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
