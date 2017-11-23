---
title: "SQLRemoveDriverManager 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRemoveDriverManager
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDriverManager
helpviewer_keywords: SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cd5658e3dfcbdad0b0ba8b8e8f12d489eadd55e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函式
**一致性**  
 版本引入： ODBC 3.0: Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更新版本的作業系統中被取代。  
  
 **摘要**  
 **SQLRemoveDriverManager**變更或移除 Odbcinst.ini 中的項目系統資訊的 ODBC 核心元件的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *pdwUsageCount*  
 [輸出]使用狀態計數的驅動程式管理員在呼叫此函式之後。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊的項目不存在，此函式呼叫時，函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriverManager**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除驅動程式管理員資訊，因為它不存在於登錄或登錄中找不到。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法以遞減的使用計數的驅動程式管理員。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriverManager**補充**SQLInstallDriverManager**函式，並且更新中的系統資訊的元件的使用計數。 應該只從安裝應用程式呼叫此函式。  
  
 **SQLRemoveDriverManager**將核心元件使用計數減 1。 如果元件使用計數變成 0，將會移除項目系統資訊。 核心元件項目是在 [系統資訊] 下的標題是"ODBC Core"中的下列位置：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  當元件使用計數和檔案的使用方式計數達到零，則應用程式應該不實際移除驅動程式管理員的檔案。  
  
 **SQLRemoveDriverManager**實際上不會移除任何檔案。 呼叫程式會負責刪除檔案和維護檔案的使用方式計數。 驅動程式管理員檔案應該不是，不過，移除，當元件使用計數和檔案使用計數已達到零，因為這些檔案可能會由其他應用程式，不會遞增檔案使用計數。  
  
 **SQLRemoveDriverManager**稱為解除安裝程序的一部分。 整個會解除安裝 ODBC 核心元件 （其中包含驅動程式管理員，資料指標程式庫，安裝程式、 語言文件庫、 系統管理員、 thunk 檔案，以及等等）。 下列檔案不會移除當**SQLRemoveDriverManager**稱為解除安裝程序的一部分：  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32。DLL|  
|ODBCCR32。DLL|ODBC16GT。DLL|  
|ODBCCU32。DLL|ODBC32GT。DLL|  
|ODBCINT。DLL|DS16GT。DLL|  
|ODBCTRAC。DLL|DS32GT。DLL|  
|MSVCRT40。DLL|ODBCAD32。EXE|  
|ODBCCP32。CPL||  
  
 **SQLRemoveDriverManager**也稱為升級的程序的一部分。 如果應用程式偵測到它必須執行升級，而且它先前已安裝驅動程式，應該移除，然後重新安裝驅動程式。  
  
 **SQLRemoveDriverManager**應該先呼叫元件使用方式計數遞減。 **SQLInstallDriverEx**然後應該呼叫以遞增的元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的核心元件檔案。 檔案使用方式計數將會維持不變，與其他應用程式使用的舊版本的核心元件檔案現在會使用較新版本的檔案。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
