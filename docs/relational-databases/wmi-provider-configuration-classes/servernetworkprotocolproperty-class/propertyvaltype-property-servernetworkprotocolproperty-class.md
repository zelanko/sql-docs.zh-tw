---
description: PropertyValType 屬性 (ServerNetworkProtocolProperty 類別)
title: 'PropertyValType 屬性 (ServerNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyValType Property (ServerNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4a74b71b3cfef263a706319ff2ac0500180497c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485161"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 屬性 (ServerNetworkProtocolProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得儲存於參考之屬性內之值的資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.PropertyValType [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表實例上網路通訊協定之屬性的 [ServerNetworkProtocolProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定屬性值之資料類型的 **uint32** 值。 如果是字串值，它會傳回 0，如果是數值類型則傳回 1。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
