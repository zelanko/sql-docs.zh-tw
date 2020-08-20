---
description: AcceptStop 屬性 (SqlService 類別)
title: 'AcceptStop 屬性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 67874a17c13c5e62dde3e364291e29516d02276f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472712"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 屬性 (SqlService 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得可指定是否可停止服務的布林屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否可停止服務的布林值：如果可以停止服務，則 **為 true** ，如果無法停止服務，則為 **false** 。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
