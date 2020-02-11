---
title: SupportAlias 屬性（ClientNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: d28ec166f8954b874f98b7f9f441280ab9064f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62826754"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 屬性 (ClientNetworkProtocol 類別)
  取得布林屬性，指定[SetOrderValue 方法（ClientNetworkProtocol 類別）](clientnetworkprotocol-class.md)所指定的目前網路通訊協定是否支援別名。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定用戶端網路通訊協定是否支援別名的布林值。  
  
 如果為 True，表示用戶端網路通訊協定支援別名。  
  
 如果為 False，表示用戶端網路通訊協定不支援別名。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
