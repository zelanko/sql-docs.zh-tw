---
title: SetOrderValue 方法（ClientNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0438ea784bc8d1521455e0d5e7b9970dafe02fd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73660092"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  從用戶端通訊協定清單中選取指定之順序值的通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*OrderValue*|設定順序值的 u**int32**值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [用戶端通訊協定屬性 (順序索引標籤)](https://technet.microsoft.com/library/ms187884.aspx)  
  
  
