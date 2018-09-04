---
title: IsSharePointIntegrated 屬性 (WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9fed6b7093b53e799bdb80e1fe50f28a516749d4
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278767"
---
# <a name="configurationsetting-property---issharepointintegrated"></a>ConfigurationSetting 屬性 - IsSharePointIntegrated
  指定報表伺服器是否處於 SharePoint 整合模式。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，此屬性一律傳回 **False** ，因為在 SharePoint 模式中， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體是 SharePoint 共用服務且不受 WMI 提供者控制。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>屬性值  
 **Boolean** 物件，指出報表伺服器是否在 SharePoint 整合模式下。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
