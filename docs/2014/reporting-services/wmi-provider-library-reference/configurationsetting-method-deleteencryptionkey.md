---
title: DeleteEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
caps.latest.revision: 20
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5b60239888c8f40e82e84fa3ae2171809cb20d70
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030213"
---
# <a name="deleteencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>DeleteEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting)
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
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  