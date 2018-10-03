---
title: SetDisable 方法 （ServerNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 0ebbe0c5-07ad-4a76-a918-e379930adf71
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7adc268cb9c12fd1ecd16a2b8b109f49d7df20e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053538"
---
# <a name="setdisable-method-servernetworkprotocol-class"></a>SetDisable 方法 (ServerNetworkProtocol 類別)
  停用伺服器網路通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ServerNetworkProtocol 類別] servernetworkprotocol-class.md) 物件，表示執行個體所使用的網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
