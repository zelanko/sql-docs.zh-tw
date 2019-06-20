---
title: ProtocolOrder 屬性 （ClientNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0a0043e5a894e3f3f1b778a6f42fe6e3bacbbc78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192890"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 屬性 (ClientNetworkProtocol 類別)
  取得目前參考的用戶端的順序號碼所指定的網路通訊協定[SetOrderValue 方法 （ClientNetworkProtocol 類別）](clientnetworkprotocol-class.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件，表示所使用的網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，可指定 `OrderValue` 方法設定之目前參考的用戶端網路通訊協定的順序號碼。 如果停用用戶端網路通訊協定，這個值將會是零。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)   
 [設定用戶端網路通訊協定和網路程式庫](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
