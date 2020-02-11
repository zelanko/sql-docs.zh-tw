---
title: SQL Server Express LocalDB 標頭 & 版本資訊
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
ms.custom: seo-dt-2019
ms.openlocfilehash: f5aeb8a5eda8e4e49e478cbc53cd0ad90e3cc890
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095471"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>SQL Server Express LocalDB 標頭和版本資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server Express LocalDB 執行個體 API 沒有個別的標頭檔；LocalDB 函數簽章和錯誤碼會定義在 SQL Server Native Client 標頭檔 (sqlncli.h) 中。 若要使用 LocalDB 執行個體 API，您必須在專案中包含 sqlncli.h 標頭檔。  
  
## <a name="localdb-versioning"></a>LocalDB 版本設定  
 LocalDB 安裝針對每個主要 SQL Server 版本使用一組二進位檔。 這些 LocalDB 版本會個別進行維護及修補。 這表示使用者必須指定所要使用的 LocalDB 基準版本 (亦即主要 SQL Server 版本)。 版本是以 .NET Framework **system.web**類別所定義的標準版本格式來指定：  
  
 *主要. 次要 [. 組建 [. 修訂]]*  
  
 版本字串（*主要*和*次要*）中的前兩個數字是強制的。 版本字串（*組建*和*修訂*）中的最後兩個數字是選擇性的，而且如果使用者離開，則預設為零。這表示如果使用者僅指定 "12.2" 做為 LocalDB 版本號碼，則會將其視為使用者指定 "12.2.0.0"。  
  
 例如，LocalDB 安裝的版本定義於 MSSQLServer\CurrentVersion 登錄機碼中的 SQL Server 執行個體登錄機碼底下，例如：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 支援在相同的工作站上並存多個 LocalDB 版本。 不過，使用者程式碼一律會使用本機電腦上最新可用的**Sqluserinstance.dll** DLL 來連接到 LocalDB 實例。  
  
## <a name="locating-the-sqluserinstance-dll"></a>尋找 SQLUserInstance DLL  
 為了找出**Sqluserinstance.dll** DLL，用戶端提供者會使用下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 在此機碼下會列出機碼清單，其中每個機碼各代表電腦上已安裝的每個 LocalDB 版本。 這些索引鍵的每一個都是以 [ * \<主要版本>*] 格式的 LocalDB 版本號碼來命名。次要版本>（例如，名為13.0 的金鑰[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ）。 * \< * 在每個版本機碼下會列出 `InstanceAPIPath` 名稱/值組，定義隨該版本安裝之 SQLUserInstance.dll 檔案的完整路徑。 下列範例顯示已安裝 LocalDB 版本11.0 和13.0 之電腦的登錄專案：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 用戶端提供者必須在所有已安裝的版本之間尋找最新**** 版本，並從相關聯`InstanceAPIPath`的值載入 sqluserinstance.dll DLL 檔案。  
  
### <a name="wow64-mode-on-64-bit-windows"></a>64 位元 Windows 上的 WOW64 模式  
 LocalDB 的 64 位元安裝包含一組額外的登錄機碼，可讓在 Windows-32-on-Windows-64 (WOW64) 模式下執行的 32 位元應用程式使用 LocalDB。 具體而言，在 64 位元 Windows 上，LocalDB MSI 會建立下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 64- `Installed Versions`讀取金鑰的程式會看到指向64位版本的**sqluserinstance.dll** DLL 的值，而 32-bit 程式（在以 WOW64 模式在64位 Windows 上執行`Installed Versions` ）會自動重新導向至位於`Wow6432Node` hive 底下的機碼。 此機碼包含指向32位版本之**Sqluserinstance.dll** DLL 的值。  
  
## <a name="using-localdb_define_proxy_functions"></a>使用 LOCALDB_DEFINE_PROXY_FUNCTIONS  
 LocalDB 實例 API 會定義名為 LOCALDB_DEFINE_PROXY_FUNCTIONS 的常數，以自動探索和載入**Sqluserinstance.dll** DLL。  
  
 此常數啟用的程式碼區段可實作每個 LocalDB API 的 Proxy。 Proxy 執行會使用通用函式系結至最新安裝的**Sqluserinstance.dll** DLL 中的進入點，然後轉送要求。  
  
 只有在包含 sqlncli.h 檔案之前，使用者程式碼中已定義常數 LOCALDB_DEFINE_PROXY_FUNCTIONS，才會啟用 Proxy 函數。 此常數應該僅定義於一個來源模組 (.cpp 檔) 中，因為該模組會為所有 API 進入點定義外部函數名稱。 此常數可以實作每個 LocalDB API 的 Proxy。  
  
 下列程式碼範例顯示如何透過原生 C++ 程式碼使用巨集：  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
