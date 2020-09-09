---
description: IsReadOnly 屬性 (SqlServiceAdvancedProperty 類別)
title: 'IsReadOnly 屬性 (SqlServiceAdvancedProperty) '
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IsReadOnly Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IsReadOnly property
ms.assetid: 9672e70f-1d8c-4133-ac73-3b5733a1c4ee
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 44dcb0a56d9c86a3957458bc570d3d1082423edd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539971"
---
# <a name="isreadonly-property-sqlserviceadvancedproperty-class"></a>IsReadOnly 屬性 (SqlServiceAdvancedProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得或設定布林屬性，該屬性會指定進階屬性是否為唯讀。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.IsReadOnly [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表進階屬性的 [SqlServiceAdvancedProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定進階屬性是否為唯讀的布林值：如果進階屬性為唯讀則為 **true** ，如果可以修改進階屬性則為 **false** 。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
