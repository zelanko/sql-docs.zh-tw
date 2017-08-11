---
title: "SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文件"
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
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d86d0c416df4ecc01f940ebabad2e409aa826599
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---setvirtualdirectory"></a>SetVirtualDirectory ConfigurationSetting 方法
  針對給定的應用程式設定虛擬目錄的名稱。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *應用程式*  
 要設定虛擬目錄之應用程式的名稱。  
  
 *VirtualDirectory*  
 虛擬目錄的名稱。  
  
 *lcid*  
 虛擬目錄的地區設定識別碼。  
  
 *錯誤*  
 [out] 發生之錯誤的描述。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。錯誤碼則表示呼叫不成功。  
  
## <a name="remarks"></a>備註  
 應用程式只能針對所有 URL 保留項目設有一個虛擬目錄名稱。  
  
 VirtualDirectory 必須符合虛擬目錄的命名慣例。 VirtualDirectory 不得為空字串或空白。  
  
 更新 \Configuration\URLReservations\Application\VirtualDirectory 元素的值。 即使尚未建立任何 URL 保留項目，也會成功。  
  
## <a name="requirements"></a>需求  
 **命名空間：**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
