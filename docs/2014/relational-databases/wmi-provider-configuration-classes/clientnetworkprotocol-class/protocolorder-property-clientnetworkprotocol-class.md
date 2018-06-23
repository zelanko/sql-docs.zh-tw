---
title: ProtocolOrder 屬性 （ClientNetworkProtocol 類別） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 388244724effee38b849742d211c446d3493d799
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030006"
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
 A [ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件，代表所使用的網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，可指定 `OrderValue` 方法設定之目前參考的用戶端網路通訊協定的順序號碼。 如果停用用戶端網路通訊協定，這個值將會是零。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)   
 [設定用戶端網路通訊協定和網路程式庫](http://technet.microsoft.com/library/ms181035.aspx)  
  
  