---
title: RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c9ab7dc3ea75201bd011b85f80169d50e2ba0d37
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518886"
---
# <a name="removeurl-method-wmi-msreportserverconfigurationsetting"></a>RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting)
  移除針對報表伺服器所保留的 URL。 如果有多個需要移除的 URL，您就必須呼叫這個 API 來逐一進行此作業。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *應用程式*  
 要移除保留項目之應用程式的名稱。  
  
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
 *UrlString* 不包含虛擬目錄名稱 - [SetVirtualDirectory 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md) 方法是針對該目的所提供。  
  
 呼叫 [ReserveURL](configurationsetting-method-reserveurl.md) 方法之前，您必須針對 *Application* 參數的 VirtualDirectory 組態屬性提供一個值。 您可以使用 [SetVirtualDirectory 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md) 方法來設定 VirtualDirectory 屬性。  
  
 如果 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了 SSL 憑證，但是沒有其他 URL 需要它，就會移除此憑證。  
  
 這個方法會導致所有非組態應用程式網域在此作業期間進行硬式回收並停止。在此作業完成之後，應用程式網域就會重新啟動。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
