---
title: SetValue 方法（ServerSettingsGeneralFlag）
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetValue Method (ServerSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: a889feac-c0e0-4635-b506-843863d86967
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b95664e8bb14ef5e66d76e7bb06140a0736a070b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888564"
---
# <a name="setvalue-method-serversettingsgeneralflag-class"></a>SetValue 方法 (ServerSettingsGeneralFlag 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定參考之旗標的所有值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示伺服器設定之一般旗標的 [ServerSettingsGeneralFlag 類別](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|*ReplTest1*|指定旗標之值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
