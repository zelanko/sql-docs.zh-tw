---
title: ProtocolDLL 屬性 （ClientNetworkProtocol 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 325d3ca62f6414ae382ba8166c79180383963021
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33008545"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>ProtocolDLL 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得所指定的網路通訊協定所需的.dll 檔案名稱[Configure Client Protocols](http://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 A [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件，代表所使用的網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定用戶端網路通訊協定所需之通訊協定 .dll 檔案的字串值。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
