---
title: DatabaseLogonType 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b58c380b85e412554eb47315dfe356d3bff08d03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097815"
---
# <a name="databaselogontype-property-wmi-msreportserverconfigurationsetting"></a>DatabaseLogonType 屬性 (WMI MSReportServer_ConfigurationSetting)
  指定報表伺服器會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>屬性值  
 代表登入類型的 `integer` 物件。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>備註  
 值為：  
  
-   0 代表 Windows 登入  
  
-   1 代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入  
  
-   2 代表要當做服務登入  
  
 如果您指定了 0 (Windows)，就必須將 [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) 屬性中的值設定為對應的有效 Windows 使用者帳戶。  
  
 如果您指定 1 (SQL Server)，請確定 [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) 的值對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 如果您指定了 2 (Windows 服務)，報表伺服器就會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帳戶和 Windows 服務帳戶來存取報表伺服器資料庫。 會忽略 DatabaseLogonAccount 屬性。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
