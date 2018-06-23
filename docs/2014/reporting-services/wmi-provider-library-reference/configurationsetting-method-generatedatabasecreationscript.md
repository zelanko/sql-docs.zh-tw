---
title: GenerateDatabaseCreationScript 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
caps.latest.revision: 25
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 05560854358e95ce4beae1727e8c1aeb7be131d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029982"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserverconfigurationsetting"></a>GenerateDatabaseCreationScript 方法 (WMI MSReportServer_ConfigurationSetting)
  產生可用來建立報表伺服器資料庫的 SQL 指令碼。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *Databasename*  
 包含要建立之報表伺服器資料庫名稱的字串。  
  
 *Lcid*  
 用於當地語系化角色名稱的值。  
  
 *IsSharePointMode*  
 指出要以原生模式或 SharePoint 模式建立資料庫。  
  
> [!IMPORTANT]  
>  從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， *IsSharePointMode* = `True` ，所以不支援在 SharePoint 模式中，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]是 SharePoint 共用服務，並且不受 WMI 提供者。 您應該一律將這個參數設定為`False`。  
  
 *指令碼*  
 [out] 包含所產生之 SQL 指令碼的字串。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 這個方法會產生 SQL 指令碼，以便針對目前所連接之報表伺服器的版本建立報表伺服器資料庫。  
  
 在 *DatabaseName* 參數中提供的值必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫命名慣例。  
  
 產生指令碼時，此方法不會檢查資料庫是否存在。  
  
 產生指令碼時，此方法不會檢查報表伺服器資料庫是否存在。  
  
 產生的指令碼支援 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  