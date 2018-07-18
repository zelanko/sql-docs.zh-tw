---
title: GetReportServerUrls 方法 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9b2963bad73fce65f252ad44ed857f6006978c2f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313194"
---
# <a name="getreportserverurls-method-wmi-msreportserverinstance"></a>GetReportServerUrls 方法 (WMI MSReportServer_Instance)
  傳回使用者可用來存取報表伺服器和報表管理員的 URL 清單。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *ApplicationName[]*  
 包含已安裝之應用程式的陣列。 值為`ReportServerWebService`或`ReportManager`。  
  
 *URLs[]*  
 包含成功註冊之 URL 的陣列。  
  
 *長度*  
 包含傳回之陣列長度的整數值。  
  
 *HRESULT*  
 表示成功的值或錯誤碼。  
  
## <a name="return-values"></a>傳回值  
  
## <a name="remarks"></a>備註  
 WMI 管理物件所公開的方法是透過 InvokeMethod 函數呼叫的。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI 文件集中的＜針對管理物件執行方法＞。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
