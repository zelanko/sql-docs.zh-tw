---
title: LocalDBGetVersionInfo 函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4350badedcaf2a4e2b977b57cf9e6cfde6c1b275
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032226"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 函數
  傳回指定之 SQL Server Express LocalDB 版本的資訊，例如此版本是否存在，以及完整的 LocalDB 版本號碼 (包括組建和發行版本號碼)。  
  
 則會傳回資訊的形式`struct`名為**LocalDBVersionInfo**，其具有下列定義。  
  
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
  
 **標頭檔：** sqlncli.h  
  
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
 [輸入]保留的大小*VersionInfo*緩衝區。  
  
## <a name="returns"></a>傳回值  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定的 LocalDB 版本不存在。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外的錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="details"></a>詳細資料  
 引進背後的原理`struct`大小引數 (*lpVersionInfoSize*) 是要讓 API 傳回的不同版本**LocalDBVersionInfostruct**，以有效地啟用新舊版相容性。  
  
 如果`struct`大小引數 (*lpVersionInfoSize*) 符合已知版本的大小**LocalDBVersionInfostruct**，該版本`struct`會傳回。 否則會傳回 LOCALDB_ERROR_INVALID_PARAMETER。  
  
 典型範例**LocalDBGetVersionInfo** API 使用方式，看起來像這樣：  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>備註  
 使用 LocalDB API 的程式碼範例，請參閱 < [SQL Server Express LocalDB 參考](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](sql-server-express-localdb-header-and-version-information.md)  
  
  
