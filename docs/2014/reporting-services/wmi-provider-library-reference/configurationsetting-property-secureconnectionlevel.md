---
title: SecureConnectionLevel 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SecureConnectionLevel
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 70b4e9e4dcaf70a34287ae6b216b9faf1749b55b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016199"
---
# <a name="secureconnectionlevel-property-wmi-msreportserverconfigurationsetting"></a>SecureConnectionLevel 屬性 (WMI MSReportServer_ConfigurationSetting)
  傳回 RSReportServer.config 檔案中指定的安全連接層級。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>屬性值  
 代表安全連接層級的 `Integer` 值。 傳回值指出 SSL 是已設定或未設定。 值大於或等於 1 時，表示 SSL 為開啟狀態。 值為 0 時，表示 SSL 為關閉狀態。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
