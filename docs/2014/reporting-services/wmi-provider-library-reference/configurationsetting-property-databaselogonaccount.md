---
title: DatabaseLogonAccount 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6b94a45ed2c528972fffb79d2f8f51ad9bcba56d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185748"
---
# <a name="databaselogonaccount-property-wmi-msreportserverconfigurationsetting"></a>DatabaseLogonAccount 屬性 (WMI MSReportServer_ConfigurationSetting)
  指定連接至報表伺服器資料庫時報表伺服器所使用的登入帳戶。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>屬性值  
 代表登入帳戶名稱的 `String` 物件。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>備註  
 此屬性的有效值取決於 windows 7 [DatabaseLogonType](configurationsetting-property-databaselogontype.md)屬性。  
  
 如果此屬性則會忽略[DatabaseLogonType](configurationsetting-property-databaselogontype.md)屬性設定為`2 (Service)`。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
