---
description: DeleteEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting)
title: DeleteEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b34f0a58d8a0c65c71b353259c5445daea0c5e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497941"
---
# <a name="configurationsetting-method---deleteencryptionkey"></a>ConfigurationSetting 方法 - DeleteEncryptionKey
  從報表伺服器資料庫中刪除加密金鑰。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>參數  
 *InstallationID*  
 位於報表伺服器資料庫之索引鍵資料表中的報表伺服器的安裝識別碼。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## <a name="return-value"></a>傳回值  
 傳回 HRESULT，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 *DeleteEncryptionKey* 方法會針對具有報表伺服器資料庫中安全資訊之存取權的任何報表伺服器，從索引鍵資料表中刪除項目。 如果指定的 *InstallationID* 參數沒有對應至資料庫中的安裝識別碼，此方法就會傳回錯誤。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
