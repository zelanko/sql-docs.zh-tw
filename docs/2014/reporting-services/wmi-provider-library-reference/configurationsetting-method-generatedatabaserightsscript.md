---
title: GenerateDatabaseRightsScript 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 575eab878e0ef9b4357c09a0a3deedf143c237b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098476"
---
# <a name="generatedatabaserightsscript-method-wmi-msreportserver_configurationsetting"></a>GenerateDatabaseRightsScript 方法 (WMI MSReportServer_ConfigurationSetting)
  產生可用來將報表伺服器資料庫和其他資料庫 (執行報表伺服器所需) 之權限授與使用者的 SQL 指令碼。 呼叫者預期要連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫伺服器並執行此指令碼。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *UserName*  
 此指令碼將授與權限之目標使用者的使用者名稱或 Windows 安全性識別碼 (SID)。  
  
 *DatabaseName*  
 此指令碼將授與使用者存取權的資料庫名稱。  
  
 *IsRemote*  
 指出資料庫是否位於報表伺服器遠端的布林值。  
  
 *IsWindowsUser*  
 指出指定之使用者名稱是 Windows 使用者或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的布林值。  
  
 *文字*  
 [out] 包含所產生之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼的字串。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 如果 *DatabaseName* 是空的，即忽略 *IsRemote* ，而且報表伺服器組態檔值會用於資料庫名稱。  
  
 如果*IsWindowsUser*設定為`true`，則*username*的格式\<應為 domain>\\<username。\>  
  
 當*IsWindowsUser*設定為`true`時，產生的腳本會將登入許可權授與的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者，並將報表伺服器資料庫設定為預設資料庫，並授與報表伺服器資料庫、報表伺服器暫存資料庫、master 資料庫和 MSDB 系統資料庫的**RSExec**角色。  
  
 當*IsWindowsUser*設定為`true`時，此方法會接受標準 Windows sid 做為輸入。 提供了標準 Windows SID 或服務帳戶名稱時，它就會轉譯成使用者名稱字串。 如果資料庫位於本機，此帳戶就會轉譯成帳戶的正確當地語系化表示。 如果資料庫位於遠端，此帳戶就會表示成電腦的帳戶。  
  
 下表將顯示已轉譯的帳戶及其遠端表示。  
  
|已轉譯的帳戶 / SID|一般名稱|遠端名稱|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|[本機系統]|
  \<網域>\\<電腦名稱\>$|  
|.\LocalSystem|[本機系統]|
  \<網域>\\<電腦名稱\>$|  
|ComputerName\LocalSystem|[本機系統]|
  \<網域>\\<電腦名稱\>$|  
|LocalSystem|[本機系統]|
  \<網域>\\<電腦名稱\>$|  
|(S-1-5-20)|網路服務|
  \<網域>\\<電腦名稱\>$|  
|NT AUTHORITY\NetworkService|網路服務|
  \<網域>\\<電腦名稱\>$|  
|(S-1-5-19)|本機服務|錯誤 - 請參閱下列內容。|  
|NT AUTHORITY\LocalService|本機服務|錯誤 - 請參閱下列內容。|  
  
 在 [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]上，如果您正在使用內建帳戶，而且報表伺服器資料庫位於遠端，就會傳回錯誤。  
  
 如果指定了 `LocalService` 內建帳戶，而且報表伺服器資料庫位於遠端，就會傳回錯誤。  
  
 當 *IsWindowsUser* 為 true，且必須轉譯 *UserName* 提供的值時，WMI 提供者就會判斷報表伺服器資料庫位於同一部電腦或遠端電腦上。 為了判斷安裝是否位於本機，WMI 提供者會根據下列值清單評估 DatabaseServerName 屬性。 如果找到相符項目，表示資料庫位於本機。 否則，就表示資料庫位於遠端。 此比較不區分大小寫。  
  
|DatabaseServerName 的值|範例|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|
  \<機器 FQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 當*IsWindowsUser*設定為`true`時，WMI 提供者會呼叫 LookupAccountName 來取得帳戶的 SID，然後呼叫 LookupAccountSID 以取得要放入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]腳本的名稱。 這樣可確保所使用的帳戶名稱會通過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 當*IsWindowsUser*設定為`false`時，產生的腳本會授與報表伺服器資料庫、報表伺服器暫存資料庫和 MSDB 資料庫上的**RSExec**角色。  
  
 當*IsWindowsUser*設定為`false`時，SQL Server 使用者必須已經存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]于中，腳本才能順利執行。  
  
 如果報表伺服器尚未指定報表伺服器資料庫，呼叫 GrantRightsToDatabaseUser 就會傳回錯誤。  
  
 產生的指令碼支援 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>需求  
 **命名空間：**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
