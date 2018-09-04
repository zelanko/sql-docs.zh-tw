---
title: ListInstalledSharePointVersions 方法 (WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f2a29d73639a811a3f79ce579f98138449a8dbf5
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280723"
---
# <a name="configurationsetting-method---listinstalledsharepointversions"></a>ConfigurationSetting 方法 - ListInstalledSharePointVersions
  傳回一組 Token，這些 Token 代表與報表伺服器安裝在同一部電腦上的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *VersionTokens[]*  
 [out] 包含一些 Token 的陣列，這些 Token 代表與已安裝之報表伺服器相容的 SharePoint 產品或技術版本。  
  
 *長度*  
 [out] 版本 Token 陣列的長度。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
 傳回的每個 Token 都代表與目前已安裝之報表伺服器相容的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 或 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 版本。 如果特定的 SharePoint 版本與先前的 SharePoint 版本相容，就會針對每個相容的 SharePoint 版本傳回 Token。  
  
 下面是所傳回 SharePoint Token 的表格。  
  
|**版本 Token**|**說明**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|已安裝與 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 相容的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、[!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、[!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 安裝。|  
|WSS_V3_Compatible|安裝了與 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3.0 相容的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 或 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 安裝。|  
|WSS_V4_Compatible|安裝了與 Office 14 相容的 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 安裝。|  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
