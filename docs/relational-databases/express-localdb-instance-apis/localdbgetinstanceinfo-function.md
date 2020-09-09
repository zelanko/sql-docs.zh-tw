---
description: LocalDBGetInstanceInfo 函數
title: LocalDBGetInstanceInfo 函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetInstanceInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 231706f5-26c6-42eb-ab47-315df6b8f824
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f5afa31d7b4b3cb814fee3df4154e713f30f7079
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544045"
---
# <a name="localdbgetinstanceinfo-function"></a>LocalDBGetInstanceInfo 函數
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  傳回指定之 SQL Server Express LocalDB 執行個體的資訊，例如執行個體是否存在、執行個體使用的 LocalDB 版本、執行個體是否正在執行等等。  
  
 這項資訊會在名為**LocalDBInstanceInfo**的結構中傳回，此**結構**具有下列定義。  
  
```  
typedef struct _LocalDBInstanceInfo  
{  
      // Contains the size of the LocalDBInstanceInfo struct  
      DWORD  cbLocalDBInstanceInfoSize;  
  
      // Holds the instance name  
      TLocalDBInstanceNamewszInstanceName;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // TRUE if the instance configuration registry is corrupted, FALSE otherwise  
      BOOLbConfigurationCorrupted;  
  
      // TRUE if the instance is running at the moment, FALSE otherwise  
      BOOL   bIsRunning;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
  
      // Holds the date and time when the instance was started for the last time  
      FILETIME ftLastStartUTC;  
  
      // Holds the name of the TDS named pipe to connect to the instance  
      WCHARwszConnection;  
  
      // TRUE if the instance is shared, FALSE otherwise  
      BOOLbIsShared;  
  
      // Holds the shared name for the instance (if the instance is shared)  
      TLocalDBInstanceNamewszSharedInstanceName;  
  
      // Holds the SID of the instance owner (if the instance is shared)  
      WCHARwszOwnerSID;   
  
      // TRUE if the instance is Automatic, FALSE otherwise  
      BOOLbIsAutomatic;  
} LocalDBInstanceInfo;  
  
```  
  
 **標頭檔：** sqlncli。h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBGetInstanceInfo(  
           PCWSTR wszInstanceName,  
           PLocalDBInstanceInfo pInstanceInfo,  
           DWORD dwInstanceInfoSize   
);  
```  
  
## <a name="parameters"></a>參數  
 *wszInstanceName*  
 [輸入] 執行個體名稱。  
  
 *pInstanceInfo*  
 [輸出] 儲存 LocalDB 執行個體資訊的緩衝區。  
  
 *dwInstanceInfoSize*  
 輸出保存 *InstanceInfo* 緩衝區的大小。  
  
## <a name="returns"></a>傳回  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定的執行個體名稱無效。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 執行個體不存在。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 應儲存執行個體的路徑長度超過 MAX_PATH。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 無法存取執行個體資料夾。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 無法存取執行個體登錄。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 執行個體組態已損毀。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="details"></a>詳細資料  
  (*lpInstanceInfoSize*) 的**結構**大小引數引進背後的原理是讓 API 傳回不同版本的**LocalDBInstanceInfostruct**，以有效地啟用向前和回溯相容性。  
  
 如果 **結構** 大小引數 (*lpInstanceInfoSize*) 符合已知 **LocalDBInstanceInfostruct**版本的大小，則會傳回該 **結構** 的版本。 否則會傳回 LOCALDB_ERROR_INVALID_PARAMETER。  
  
 **LocalDBGetInstanceInfo** API 使用方式的典型範例如下所示：  
  
```  
LocalDBInstanceInfo ii;  
LocalDBInstanceInfo(L"Test", &ii, sizeof(LocalDBInstanceInfo));  
  
```  
  
 如需使用 LocalDB API 的程式碼範例，請參閱 [SQL Server Express Localdb 參考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
