---
description: SetNumValue 方法 (SqlServiceAdvancedProperty 類別)
title: 'SetNumValue 方法 (SqlServiceAdvancedProperty) '
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumValue method
ms.assetid: a5e1056b-0b75-4ad6-99c1-89246010d815
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1e9c06349348b24e58f16644fa77dfd602a7570b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545216"
---
# <a name="setnumvalue-method-sqlserviceadvancedproperty-class"></a>SetNumValue 方法 (SqlServiceAdvancedProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定屬性的數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetNumValue(NumValue)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表進階屬性的 [SqlServiceAdvancedProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*NumValue*|指定 advanced 屬性值的 **uint32** 值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
 屬性值類型必須是數值，才能將屬性設定為數值。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
