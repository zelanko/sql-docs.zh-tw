---
title: SetEnable 方法（ClientNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f3f92e3b417b3f669cc621e2d29c8ece24183af4
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660121"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 方法 (ClientNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  啟用[設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)所指定的用戶端網路通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetEnableMethod()  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
