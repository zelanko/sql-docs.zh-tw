---
title: InitializeReportServer 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f5ea9e6e4e36e62828f3036c3765ba42c202448c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098350"
---
# <a name="initializereportserver-method-wmi-msreportserver_configurationsetting"></a>InitializeReportServer 方法 (WMI MSReportServer_ConfigurationSetting)
  初始化指定的報表服務執行個體。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>參數  
 *InstallationID*  
 用來在傳回加密金鑰之前進行加密的字串。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 呼叫這個方法時，系統會使用 *InstallationID*所識別之報表伺服器的公開金鑰來加密存取報表伺服器資料庫安全資訊的加密金鑰。  
  
 所指定報表伺服器的公開金鑰必須已經事先寫入報表伺服器資料庫中。  
  
 您必須針對已經擁有安全資訊之存取權的報表伺服器呼叫 *InitializeReportServer* 方法，才能讓它解密加密金鑰。 然後，所產生且已加密的加密金鑰密就會儲存在報表伺服器資料庫中。  
  
 如果在呼叫 InitializeReportServer 方法[IsInitialized](configurationsetting-property-isinitialized.md)時，報表伺服器的`true` IsInitialized 屬性設定為，則方法會傳回成功，而不會嘗試加密加密金鑰。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
