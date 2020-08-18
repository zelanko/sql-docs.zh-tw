---
description: LocalDBGetVersionInfo 函數
title: LocalDBGetVersionInfo 函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c4e39c8bf22b4baeccfdd782d48fde7be342f68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408744"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 函數
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  傳回指定之 SQL Server Express LocalDB 版本的資訊，例如此版本是否存在，以及完整的 LocalDB 版本號碼 (包括組建和發行版本號碼)。  
  
 這項資訊會以名為**LocalDBVersionInfo**的**結構**形式傳回，此結構具有下列定義。  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **標頭檔：** sqlncli。h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>參數  
 *wszVersionName*  
 [輸入] LocalDB 版本名稱。  
  
 *pVersionInfo*  
 [輸出] 儲存 LocalDB 版本資訊的緩衝區。  
  
 *dwVersionInfoSize*  
 輸出保存 *VersionInfo* 緩衝區的大小。  
  
## <a name="returns"></a>傳回  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定的 LocalDB 版本不存在。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="details"></a>詳細資料  
  (*lpVersionInfoSize*) 的**結構**大小引數引進背後的原理是讓 API 傳回不同版本的**LocalDBVersionInfostruct**，以有效地啟用向前和回溯相容性。  
  
 如果 **結構** 大小引數 (*lpVersionInfoSize*) 符合已知 **LocalDBVersionInfostruct**版本的大小，則會傳回該 **結構** 的版本。 否則會傳回 LOCALDB_ERROR_INVALID_PARAMETER。  
  
 **LocalDBGetVersionInfo** API 使用方式的典型範例如下所示：  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>備註  
 如需使用 LocalDB API 的程式碼範例，請參閱 [SQL Server Express Localdb 參考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
