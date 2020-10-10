---
description: ProtocolDLL 屬性 (ClientNetworkProtocol 類別)
title: 'ProtocolDLL 屬性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 54d992dd3d9b3604644f985f9e7db5f523b553f9
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888926"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>ProtocolDLL 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得 [設定用戶端通訊](../../../database-engine/configure-windows/configure-client-protocols.md)協定所指定之網路通訊協定所需的 .DLL 檔案名。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定用戶端網路通訊協定所需之通訊協定 .dll 檔案的字串值。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
