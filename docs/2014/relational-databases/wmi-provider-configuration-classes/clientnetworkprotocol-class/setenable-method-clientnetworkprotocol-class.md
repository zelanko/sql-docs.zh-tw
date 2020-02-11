---
title: SetEnable 方法（ClientNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1aa192f2dc78a424b1d4c8792044caac0934173a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62826718"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 方法 (ClientNetworkProtocol 類別)
  啟用[設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)所指定的用戶端網路通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetEnableMethod()  
  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端所使用之網路通訊協定的[ClientNetworkProtocol 類別](clientnetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 
  `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端網路通訊協定和網路程式庫](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
