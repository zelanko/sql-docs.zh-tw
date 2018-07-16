---
title: SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8808b7ccaf08ecbaad2b124853425c5b1f2792c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181545"
---
# <a name="setdatabaseconnection-method-wmi-msreportserverconfigurationsetting"></a>SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="remarks"></a>備註  
 當 *CredentialsType* 參數設為 0 時 (Windows)，即必須設定 *UserName* 和 *Password* 參數。 *UserName* 參數必須採用「網域\使用者名稱」格式，且此值必須代表有效的 Windows 登入。  
  
 當 *CredentialsType* 參數設為 1 時 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，傳入 *UserName* 參數的值必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱的需求。  
  
 當 *CredentialsType* 參數設為 2 時 (Windows 服務)，報表伺服器就會使用整合式安全性來連接至報表伺服器資料庫，並忽略 *UserName* 和 *Password* 參數。 報表伺服器 Web 服務將會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帳戶或應用程式集區的帳戶和 Windows 服務帳戶來存取報表伺服器資料庫。  
  
 SetDatabaseConnection 方法一經呼叫，就會在指定之報表伺服器的組態檔中加密並儲存認證和資料庫資訊。  
  
 SetDatabaseConnection 方法不會檢查報表伺服器是否能夠使用指定的資料來連接至報表伺服器資料庫。  
  
 第一次設定時，ConnectionPoolSize 屬性是根據下列處理器設定的：ConnectionPoolSize = #Processors * 75。  
  
 SetDatabaseConnection 方法不會將權限授與指定的帳戶。 您必須呼叫[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)每個帳戶都需要存取報表伺服器資料庫，並執行所產生的指令碼的方法。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
