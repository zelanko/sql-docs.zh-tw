---
title: ProtocolName 屬性（ClientNetworkProtocol）
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: beb51ea7270fdbeb96dc858c2ef4e65c386726ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73660236"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName 屬性 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得[設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)所指定的目前網路通訊協定名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 字串值，指定[SetOrderValue 方法（ClientNetworkProtocol 類別）](https://technet.microsoft.com/library/ms179295.aspx)所參考之目前用戶端網路通訊協定的名稱。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
