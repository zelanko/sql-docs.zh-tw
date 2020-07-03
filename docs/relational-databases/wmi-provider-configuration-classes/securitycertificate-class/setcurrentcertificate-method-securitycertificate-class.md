---
title: SetCurrentCertificate 方法（SecurityCertificate）
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7997103a062ac796ead5694befd1d9cebb600c95
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888793"
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>SetCurrentCertificate 方法 (SecurityCertificate 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  設定目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表安全性憑證的 [SecurityCertificate 類別](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|*SHA*|針對必要安全性憑證指定安全雜湊演算法 (SHA) 指模的字串值。|  
|*SQLInstance*|指定需要憑證之執行個體的字串值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
