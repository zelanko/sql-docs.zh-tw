---
title: "SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d570b4d32481e15ce78bef98c97b7330192f1c8c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>ConfigurationSetting 方法 - SetDatabaseConnection
  設定特定報表伺服器資料庫的報表伺服器資料庫連接。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *Server*  
 用來主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
 *DatabaseName*  
 報表伺服器資料庫的名稱。  
  
 *CredentialsType*  
 要用於連接的認證類型。 其值可能是：  
  
-   0 - Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Windows 服務  
  
 *UserName*  
 用來連接至報表伺服器資料庫的帳戶名稱。  
  
 *密碼*  
 用來連接至報表伺服器資料庫的密碼。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
 當 *CredentialsType* 參數設為 0 時 (Windows)，即必須設定 *UserName* 和 *Password* 參數。 *UserName* 參數必須採用「網域\使用者名稱」格式，且此值必須代表有效的 Windows 登入。  
  
 當 *CredentialsType* 參數設為 1 時 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，傳入 *UserName* 參數的值必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱的需求。  
  
 當 *CredentialsType* 參數設為 2 時 (Windows 服務)，報表伺服器就會使用整合式安全性來連接至報表伺服器資料庫，並忽略 *UserName* 和 *Password* 參數。 報表伺服器 Web 服務將會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帳戶或應用程式集區的帳戶和 Windows 服務帳戶來存取報表伺服器資料庫。  
  
 SetDatabaseConnection 方法一經呼叫，就會在指定之報表伺服器的組態檔中加密並儲存認證和資料庫資訊。  
  
 SetDatabaseConnection 方法不會檢查報表伺服器是否能夠使用指定的資料來連接至報表伺服器資料庫。  
  
 第一次設定時，ConnectionPoolSize 屬性是根據下列處理器設定的：ConnectionPoolSize = #Processors * 75。  
  
 SetDatabaseConnection 方法不會將權限授與指定的帳戶。 您必須針對需要存取報表伺服器資料庫的每個帳戶呼叫 [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) 方法，並且執行產生的指令碼。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
