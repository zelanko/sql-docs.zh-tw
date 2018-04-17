---
title: ProtocolOrder 屬性 （ClientNetworkProtocol 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9804106693da8b5f3a60cecf6d2182b5c9a9e75c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得目前參考的用戶端的順序號碼所指定的網路通訊協定[SetOrderValue 方法 （ClientNetworkProtocol 類別）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 A [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件，代表所使用的網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，指定所設定之目前參考的用戶端網路通訊協定的順序號碼**OrderValue**方法。 如果停用用戶端網路通訊協定，這個值將會是零。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)   
 [設定用戶端網路通訊協定和網路程式庫](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
