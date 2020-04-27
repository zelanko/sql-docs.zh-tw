---
title: IsSharePointIntegrated 屬性 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 95e7bade956c791feceddc32f2a0423c331fe77f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097104"
---
# <a name="issharepointintegrated-property-wmi-msreportserver_instance"></a>IsSharePointIntegrated 屬性 (WMI MSReportServer_Instance)
  指定報表伺服器是否處於 SharePoint 整合模式。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，此屬性一律傳回 `False`，因為在 SharePoint 模式中，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體是 SharePoint 共用服務且不受 WMI 提供者控制。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>屬性值  
 指出報表伺服器是否處於 SharePoint 整合模式的 `Boolean` 值。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_Instance 成員](msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
  
