---
title: SupportAlias 屬性 （ClientNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2bfb677ba05bc5303c706d65dd2dda70eb67d23d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082568"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 屬性 (ClientNetworkProtocol 類別)
  取得布林屬性，指定目前的網路所指定的通訊協定是否[SetOrderValue 方法 （ClientNetworkProtocol 類別）](clientnetworkprotocol-class.md)支援別名。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件，表示所使用的網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定用戶端網路通訊協定是否支援別名的布林值。  
  
 如果為 True，表示用戶端網路通訊協定支援別名。  
  
 如果為 False，表示用戶端網路通訊協定不支援別名。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
