---
title: SQLConfigData源函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90a51193a8f4edbb013527c4dde0625b75131583
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299628"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 函數 (英文)
**一致性**  
 版本介紹: ODBC 1.0  
  
 **摘要**  
 **SQLConfigDataSource**添加、修改或刪除資料來源。  
  
 **SQLConfigDataSource**的功能也可以與[ODBCCONF 一起訪問。EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd 家長*  
 [輸入]父視窗句柄。 如果句柄為空,則函數將不會顯示任何對話方塊。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*參數必須包含以下值之一:  
  
 ODBC_ADD_DSN:添加新的用戶數據源。  
  
 ODBC_CONFIG_DSN:配置(修改)現有用戶數據源。  
  
 ODBC_REMOVE_DSN:刪除現有用戶數據源。  
  
 ODBC_ADD_SYS_DSN:添加新的系統數據源。  
  
 ODBC_CONFIG_SYS_DSN:修改現有系統數據源。  
  
 ODBC_REMOVE_SYS_DSN:刪除現有系統數據源。  
  
 ODBC_REMOVE_DEFAULT_DSN:從系統資訊中刪除預設數據源規範部分。 (它還從系統資訊中的 Odbcinst.ini 條目中刪除預設驅動程序規範部分。 此*fRequest*執行的功能與棄用的**SQLRemoveDefaultDataSource**函數相同。指定此選項後,對**SQLConfigDataSource**的調用中的所有其他參數應為 NUL;對 SQL 呼叫時,所有其他參數都應為 NUL。如果它們不是 NULL,則將被忽略。  
  
 *lpszDriver*  
 [輸入]向使用者而不是物理驅動程式名稱顯示的驅動程式描述(通常是關聯的 DBMS 的名稱)。  
  
 *lpsz屬性*  
 [輸入]以關鍵字-值對形式加倍終止的屬性清單。 有關詳細資訊,請參閱[設定DSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。 如果在調用此函數時系統資訊中不存在條目,則函數將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDataSource**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效或 NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_ADD_DSNODBC_CONFIG_DSN ODBC_REMOVE_DSNODBC_ADD_SYS_DSNODBC_CONFIG_SYS_DSNODBC_REMOVE_SYS_DSNODBC_REMOVE_DEFAULT_DSNODBC_CONFIG_DSN|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。 在註冊表中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效關鍵字-值對|*lpszAttributes*參數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行*fRequest*參數請求的操作。 對**ConfigDSN 的**調用失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉換器設定庫|無法載入驅動程式設置庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDataSource**使用*lpszDriver*的值從系統資訊讀取驅動程式的安裝程式 DLL 的完整路徑。 它載入 DLL 並呼叫**ConfigDSN,** 其參數與傳遞給它的相同參數相同。  
  
 **如果 SQLConfigDataSource**無法查找或載入安裝程式 DLL 或使用者取消對話框,則返回 FALSE。 否則,它將返回從**ConfigDSN**收到的狀態。  
  
 **SQLConfigDataSource**將系統 DSN *fRequest*映射到使用者 DSN *fRequests(ODBC_ADD_SYS_DSN*到ODBC_ADD_DSN,ODBC_CONFIG_SYS_DSN到ODBC_CONFIG_DSN,ODBC_REMOVE_SYS_DSN到ODBC_REMOVE_DSN)。 為了區分使用者和系統**DSN,SQLConfigDataSource**根據下表設置安裝程式配置模式。 在返回之前 **,SQLConfigDataSource**會將配置模式重置為 BOTHDSN。 **配置DSN(** 由驅動程式實現)應呼叫**SQLWriteDSNToini**和**SQLWritePrivateProfileString**來支援系統 DSN。 有關詳細資訊,請參閱[配置DSN函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*f 要求*|設定模式|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除資料來源|[設定DSN(](../../../odbc/reference/syntax/configdsn-function.md)在設定 DLL 中 )|  
|從系統資訊中移除資料來源名稱|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|新增資料來源名稱|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
