---
title: "InitializeReportServer 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
caps.latest.revision: "21"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cc11b7a514b96c08cc87f8563977dadb9fb71cf8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---initializereportserver"></a>ConfigurationSetting 方法 - InitializeReportServer
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
  
 指定之報表伺服器的公開金鑰必須已經事先寫入報表伺服器資料庫中。  
  
 您必須針對已經擁有安全資訊之存取權的報表伺服器呼叫 *InitializeReportServer* 方法，才能讓它解密加密金鑰。 然後，所產生且已加密的加密金鑰密就會儲存在報表伺服器資料庫中。  
  
 如果呼叫 InitializeReportServer 方法時，報表伺服器的 [IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md) 屬性設定為 **true** ，此方法就會傳回成功但不會嘗試加密加密金鑰。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
