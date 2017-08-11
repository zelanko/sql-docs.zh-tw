---
title: "SMTPServer 屬性 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文件"
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
apiname:
- SMTPServer
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SMTPServer property
ms.assetid: 8bcceeba-e1a0-44ef-bda1-600c6925e1db
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9034d6214aa4dfb15c9111393ca57fffcf7b1d8f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-property---smtpserver"></a>ConfigurationSetting 屬性-SMTPServer
  從報表伺服器組態檔中取得 SMTP 伺服器屬性。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim SMTPServer As String  
```  
  
```csharp  
public string SMTPServer;  
```  
  
## <a name="property-values"></a>屬性值  
 唯讀 **String** 物件，包含 RSReportServer.config 檔中的 **SMTPServer** 屬性值。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
