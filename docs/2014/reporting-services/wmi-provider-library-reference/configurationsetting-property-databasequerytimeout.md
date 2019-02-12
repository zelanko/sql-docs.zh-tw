---
title: DatabaseQueryTimeout 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseQueryTimeout Property
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cf21ba6211a016676ea7d1f2547bf4d96b1e6fb4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023760"
---
# <a name="databasequerytimeout-property-wmi-msreportserverconfigurationsetting"></a>DatabaseQueryTimeout 屬性 (WMI MSReportServer_ConfigurationSetting)
  指定在報表伺服器認定命令失敗，或是花太多時間執行之前必須經過的秒數。 報表伺服器會針對 SQL 目錄，而不是報表資料來源排定查詢的時間。 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>屬性值  
 代表查詢允許執行之秒數的 32 位元不帶正負號的 `integer` 物件。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
