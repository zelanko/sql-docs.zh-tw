---
title: GenerateDatabaseUpgradeScript 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseUpgradeScript method
ms.assetid: 88534e8e-2877-41cd-b5c2-b1d33a0fd203
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f97761fb6966de21dee53779869128b521f49840
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---generatedatabaseupgradescript"></a>ConfigurationSetting 方法 - GenerateDatabaseUpgradeScript
  產生可用來將報表伺服器資料庫升級至 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 結構描述的指令碼。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub GenerateDatabaseUpgradeScript(DatabaseName as String, _  
    ServerVersion as String, ByRef Script as String, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GenerateDatabaseUpgradeScript (string DatabaseName,   
    string ServerVersion, out string Script,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *Databasename*  
 包含要升級之報表伺服器資料庫名稱的字串。  
  
 *ServerVersion*  
 包含報表伺服器版本的字串。  
  
 *指令碼*  
 [out] 包含所產生之 SQL 指令碼的字串。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
 產生的指令碼支援 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
