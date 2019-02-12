---
title: DatabaseLogonAccount 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c9192e0845a5a6df9c7b848a3f91368dd15cfc60
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025059"
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
 這個屬性的有效值會因 [DatabaseLogonType](configurationsetting-property-databaselogontype.md) 屬性的值而不同。  
  
 如果此屬性則會忽略[DatabaseLogonType](configurationsetting-property-databaselogontype.md)屬性設定為`2 (Service)`。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
