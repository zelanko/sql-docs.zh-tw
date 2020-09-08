---
description: ProtocolOrder 屬性 (ClientNetworkProtocol 類別)
title: 'ProtocolOrder 屬性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51b686edb6ac9e93862c5f90f06bb7370fe47a9a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89522799"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得目前參考的用戶端網路通訊協定的順序號碼，如同 [SetOrderValue 方法 (ClientNetworkProtocol 類別) ](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) 方法所指定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表用戶端所使用之網路通訊協定的 [ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，指定**OrderValue**方法所設定之目前參考用戶端網路通訊協定的順序號碼。 如果停用用戶端網路通訊協定，這個值將會是零。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)   
 [設定用戶端網路通訊協定和網路程式庫](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
