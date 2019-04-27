---
title: ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ReservedURL method
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aaae1838f9af2040105e85bd0dd7fdc82ac442d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646444"
---
# <a name="reserveurl-method-wmi-msreportserverconfigurationsetting"></a>ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting)
  加入給定應用程式的 URL 保留項目。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *應用程式*  
 要保留 URL 之應用程式的名稱。  
  
 *URLString*  
 保留項目的 URL。  
  
 *lcid*  
 要用於傳回之錯誤訊息的地區設定。  
  
 *錯誤*  
 [out] 發生之錯誤的描述。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。錯誤碼則表示呼叫不成功。  
  
## <a name="remarks"></a>備註  
 *UrlString* 不包含虛擬目錄名稱。 [SetVirtualDirectory](configurationsetting-method-setvirtualdirectory.md) 方法是針對該目的提供的。  
  
 URL 保留項目是針對目前的 Windows 服務帳戶所建立的。 變更 Windows 服務帳戶需要手動更新所有 URL 保留項目。  
  
 這個方法會導致所有應用程式網域進行硬式回收。 在此作業完成之後，應用程式網域就會重新啟動。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
