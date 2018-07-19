---
title: SMTPServer 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- SMTPServer
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SMTPServer property
ms.assetid: 8bcceeba-e1a0-44ef-bda1-600c6925e1db
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 18a199fd258b5a04b9fed3bf0167b4460d99c368
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185695"
---
# <a name="smtpserver-property-wmi-msreportserverconfigurationsetting"></a>SMTPServer 屬性 (WMI MSReportServer_ConfigurationSetting)
  從報表伺服器組態檔中取得 SMTP 伺服器屬性。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim SMTPServer As String  
```  
  
```csharp  
public string SMTPServer;  
```  
  
## <a name="property-values"></a>屬性值  
 唯讀 `String` 物件，包含 RSReportServer.config 檔中的 `SMTPServer` 屬性值。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
