---
title: SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 72223544c4fc461f99413658df5ae15b5404b0b5
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279120"
---
# <a name="configurationsetting-method---setemailconfiguration"></a>ConfigurationSetting 方法 - SetEmailConfiguration
  設定報表伺服器用來傳送電子郵件的電子郵件傳遞延伸模組。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *SendUsingSMTPServer*  
 指出伺服器是否要使用 SMTP 伺服器來傳送電子郵件的布林值。 這個值只能設定為 true。 預設值為 false。  
  
 *SMTPServer*  
 包含 SMTP 伺服器之名稱或 IP 位址的字串。  
  
 *SenderEmailAddress*  
 在報表伺服器所傳送的電子郵件中，用於「寄件者:」欄位的電子郵件地址。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
 當 *SendUsingSMTPServer* 參數設定為 **true**時，報表伺服器組態檔中的 **SendUsing** 項目就會設定為 1。 當 *SendUsingSMTPServer* 設定為 **false**時，就不會設定 **SendUsing** 項目。  
  
 這個方法無法讓使用者將報表伺服器組態檔中的 **SendUsing** 項目設定為 1 以外的值。 若要針對 SMTP 郵件以外的任何項目設定報表伺服器，您必須手動編輯此組態檔。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
