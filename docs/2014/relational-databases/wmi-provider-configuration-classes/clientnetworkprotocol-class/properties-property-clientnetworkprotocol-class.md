---
title: Properties 屬性 （ClientNetworkProtocol 類別） |Microsoft 文件
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
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4882f26e1f74fd68e67f14172482bcc674d1b06e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031818"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 屬性 (ClientNetworkProtocol 類別)
  取得與所指定之目前用戶端網路通訊協定相關聯的屬性[Configure Client Protocols](http://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件，代表所使用的網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 陣列[ClientNetworkProtocolProperty 類別](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)代表所參考之目前用戶端網路通訊協定所支援之屬性的物件`OrderValue`屬性。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](http://technet.microsoft.com/library/ms181035.aspx)  
  
  