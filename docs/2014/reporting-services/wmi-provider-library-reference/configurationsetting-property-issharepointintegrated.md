---
title: IsSharePointIntegrated 屬性 (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 1b3b3ca2c450531b6bf7ef5c1a5a6ed4d06a63b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134859"
---
# <a name="issharepointintegrated-property-wmi"></a>IsSharePointIntegrated 屬性 (WMI)
  指定報表伺服器是否處於 SharePoint 整合模式。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，此屬性一律傳回 `False`，因為在 SharePoint 模式中，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體是 SharePoint 共用服務且不受 WMI 提供者控制。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>屬性值  
 `Boolean` 物件，指出報表伺服器是否在 SharePoint 整合模式下。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  