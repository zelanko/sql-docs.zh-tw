---
description: GetCurrentCertificate 方法 (ServerSettings 類別)
title: 'GetCurrentCertificate 方法 (ServerSettings) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 450e33c6-91d4-420f-ab7c-1905111f5658
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e2c9733194cc8d060caf1fa535ae685b64945de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485131"
---
# <a name="getcurrentcertificate-method-serversettings-class"></a>GetCurrentCertificate 方法 (ServerSettings 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.GetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示實例上之伺服器設定的 **ServerSettings** 物件 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*SHA*|在方法完成之後指定目前安全性憑證的字串物件值 (輸出參數)。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
