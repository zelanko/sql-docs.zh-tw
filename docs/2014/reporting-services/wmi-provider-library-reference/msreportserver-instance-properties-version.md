---
title: Version 屬性 (WMI MSReportServer_Instance) | Microsoft Docs
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
- Version property
ms.assetid: eea6bfe9-3130-4272-b3c2-c334349a7afd
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ad85fe878b81dd603cb925b187371292509ab87e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036023"
---
# <a name="version-property-wmi-msreportserverinstance"></a>Version 屬性 (WMI MSReportServer_Instance)
  以 Major.Minor.Build.Revision 的格式傳回報表伺服器的版本。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim Version As String  
```  
  
```csharp  
public string Version;  
```  
  
## <a name="property-value"></a>屬性值  
 A`string`其中包含報表伺服器的版本。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_Instance 成員](msreportserver-instance-members.md)  
  
  