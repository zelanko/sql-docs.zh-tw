---
title: "IsSharePointIntegrated 屬性 (WMI MSReportServer_Instance) |Microsoft 文件"
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
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a4a86ce7dbb8336aaa70cb2f93debe5dd7f9f70f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="msreportserverinstance-properties---issharepointintegrated"></a>MSReportServer_Instance 屬性-IsSharePointIntegrated
  指定報表伺服器是否處於 SharePoint 整合模式。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，此屬性一律傳回 **False** ，因為在 SharePoint 模式中， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體是 SharePoint 共用服務且不受 WMI 提供者控制。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>屬性值  
 指出報表伺服器是否處於 SharePoint 整合模式的 **Boolean** 值。  
  
## <a name="requirements"></a>需求  
 **命名空間：**[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [MSReportServer_Instance 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
