---
title: SecureConnectionLevel 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42beaf5446038bfaa0faf1b8e95a4eb5fc6d16b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727896"
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
 代表安全連接層級的 **Integer** 值。 傳回值指出 SSL 是已設定或未設定。 值大於或等於 1 時，表示 SSL 為開啟狀態。 值為 0 時，表示 SSL 為關閉狀態。  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks

在 SQL Server 2008 R2 中，SecureConnectionLevel 會變成 on/off 開關。 如需詳細資訊，請參閱 [ConfigurationSetting 方法 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)。

## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
