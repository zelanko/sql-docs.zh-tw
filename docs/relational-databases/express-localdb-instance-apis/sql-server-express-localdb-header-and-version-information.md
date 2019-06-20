---
title: SQL Server Express LocalDB 標頭和版本資訊 |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 870acddcd825c9c112274d294fa4c97848a85236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669653"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>SQL Server Express LocalDB 標頭和版本資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server Express LocalDB 執行個體 API 沒有個別的標頭檔；LocalDB 函數簽章和錯誤碼會定義在 SQL Server Native Client 標頭檔 (sqlncli.h) 中。 若要使用 LocalDB 執行個體 API，您必須在專案中包含 sqlncli.h 標頭檔。  
  
## <a name="localdb-versioning"></a>LocalDB 版本設定  
 LocalDB 安裝針對每個主要 SQL Server 版本使用一組二進位檔。 這些 LocalDB 版本會個別進行維護及修補。 這表示使用者必須指定所要使用的 LocalDB 基準版本 (亦即主要 SQL Server 版本)。 .NET Framework 所定義的標準版本格式指定版本，則**System.Version**類別：  
  
 *major.minor[.build[.revision]]*  
  
 版本字串的前兩個數字 (*主要*並*次要*) 是必要項目。 版本字串的最後兩個數字 (*建置*並*修訂*) 為選擇性，預設為零，如果使用者離開其。這表示，如果使用者僅指定"12.2"做為 LocalDB 版本號碼，則會被視為使用者指定"12.2.0.0"。  
  
 例如，LocalDB 安裝的版本定義於 MSSQLServer\CurrentVersion 登錄機碼中的 SQL Server 執行個體登錄機碼底下，例如：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 支援在相同的工作站上並存多個 LocalDB 版本。 不過，使用者程式碼一律使用最新可用**SQLUserInstance** DLL 在本機電腦上的連接到 LocalDB 執行個體。  
  
## <a name="locating-the-sqluserinstance-dll"></a>尋找 SQLUserInstance DLL  
 若要找出**SQLUserInstance** DLL 時，用戶端提供者會使用下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 在此機碼下會列出機碼清單，其中每個機碼各代表電腦上已安裝的每個 LocalDB 版本。 每個這些金鑰使用 LocalDB 版本號碼的格式命名 *\<主要版本 >* 。 *\<次要版本 >* (例如，索引鍵[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]名為 13.0)。 在每個版本機碼下會列出 `InstanceAPIPath` 名稱/值組，定義隨該版本安裝之 SQLUserInstance.dll 檔案的完整路徑。 下列範例示範 LocalDB 11.0 和 13.0 安裝的版本的電腦的登錄項目：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 用戶端提供者必須尋找所有已安裝的版本和負載之間的最新版本**SQLUserInstance**從相關聯的 DLL 檔案`InstanceAPIPath`值。  
  
### <a name="wow64-mode-on-64-bit-windows"></a>64 位元 Windows 上的 WOW64 模式  
 LocalDB 的 64 位元安裝包含一組額外的登錄機碼，可讓在 Windows-32-on-Windows-64 (WOW64) 模式下執行的 32 位元應用程式使用 LocalDB。 具體而言，在 64 位元 Windows 上，LocalDB MSI 會建立下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 64 位元程式讀取`Installed Versions`金鑰會看到指向 64 位元版本的值**SQLUserInstance** DLL，而 32 位元程式 （64 位元 Windows，在 WOW64 模式中執行） 會自動重新導向至`Installed Versions`機碼位於`Wow6432Node`hive。 此機碼包含指向 32 位元版本的值**SQLUserInstance** DLL。  
  
## <a name="using-localdbdefineproxyfunctions"></a>使用 LOCALDB_DEFINE_PROXY_FUNCTIONS  
 LocalDB 執行個體 API 定義名為 LOCALDB_DEFINE_PROXY_FUNCTIONS，會自動探索並載入**SqlUserInstance** DLL。  
  
 此常數啟用的程式碼區段可實作每個 LocalDB API 的 Proxy。 此 proxy 實作使用常見的函式繫結至在已安裝最新的進入點**SqlUserInstance** DLL，再將轉送要求。  
  
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
  
  
