---
description: SetValue 方法 (ClientSettingsGeneralFlag 類別)
title: ClientSettingsGeneralFlag) 的 SetValue 方法 (
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetValue Method (ClientSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: 34443689-a0e0-4668-a811-17532c6fd271
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ceab1e91f11cdb53ed157d595260b1fb448a453f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545293"
---
# <a name="setvalue-method-clientsettingsgeneralflag-class"></a>SetValue 方法 (ClientSettingsGeneralFlag 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定參考之旗標的所有值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示伺服器設定之一般旗標的 [ClientSettingsGeneralFlag 類別](../../../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*值*|指定旗標之值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
