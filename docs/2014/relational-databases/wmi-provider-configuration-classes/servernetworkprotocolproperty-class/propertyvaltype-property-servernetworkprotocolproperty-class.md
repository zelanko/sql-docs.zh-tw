---
title: PropertyValType 屬性（ServerNetworkProtocolProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4a69cb8f0817c086537381a87b96dfb237b8d59c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62643190"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 屬性 (ServerNetworkProtocolProperty 類別)
  取得儲存於參考之屬性內之值的資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 代表實例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上網路通訊協定之屬性的[ServerNetworkProtocolProperty 類別](servernetworkprotocolproperty-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定屬性值之資料類型的 `uint32` 值。 如果是字串值，它會傳回 0，如果是數值類型則傳回 1。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
