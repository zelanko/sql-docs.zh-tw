---
title: SecureConnectionLevel 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 59c833c86c632c0f5a0838a98f31d89f4f0df5fb
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635867"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting 屬性 - SecureConnectionLevel
  傳回 RSReportServer.config 檔案中指定的安全連接層級。 唯讀。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>屬性值  
 代表安全連接層級的 **Integer** 值。 傳回值指出 TLS 是已設定或未設定。 值大於或等於 1 時，表示 TLS 為開啟狀態。 值為 0 時，表示 TLS 為關閉狀態。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>備註

在 SQL Server 2008 R2 中，SecureConnectionLevel 會變成 on/off 開關。 如需詳細資訊，請參閱 [ConfigurationSetting 方法 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)。

## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
