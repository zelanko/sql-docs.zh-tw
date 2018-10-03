---
title: SQLRemoveDriverManager 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa90a3ec804717ff23c249b8a54e23665933f1a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794266"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函式
**合規性**  
 版本引入： ODBC 3.0： 在 Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更新版本的作業系統中已被取代。  
  
 **摘要**  
 **SQLRemoveDriverManager**變更或移除 Odbcinst.ini 中的項目系統資訊中的 ODBC 核心元件的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *pdwUsageCount*  
 [輸出]使用量的驅動程式管理員在呼叫此函式之後。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊 中的項目不存在，此函式呼叫時，此函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriverManager**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到的元件|安裝程式無法移除驅動程式管理員資訊，因為它不存在登錄中，或找不到登錄中。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減的元件使用計數|安裝程式無法在驅動程式管理員 的使用方式計數遞減。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriverManager**補充**SQLInstallDriverManager**函式，並且更新中的系統資訊的元件的使用計數。 只能從安裝應用程式，就應該呼叫此函式。  
  
 **SQLRemoveDriverManager**會減 1 的核心元件的使用計數。 如果元件使用計數變成 0，將會移除的項目系統資訊。 核心元件項目是在系統資訊中，標題為 「 ODBC 核心 」 底下的下列位置：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  當元件使用計數和檔案的使用方式計數到達零，則應用程式應該不實際移除驅動程式管理員的檔案。  
  
 **SQLRemoveDriverManager**實際上不會移除任何檔案。 呼叫程式會負責刪除檔案，並維護檔案使用量計算。 驅動程式管理員的檔案應該不是，不過，移除時的元件使用計數和檔案使用計數已達到零，因為這些檔案可能由其他應用程式，不會遞增檔案使用計數。  
  
 **SQLRemoveDriverManager**稱為解除安裝程序的一部分。 ODBC 核心元件 （包括驅動程式管理員、 資料指標程式庫、 安裝程式、 語言程式庫，系統管理員、 thunk 檔案等等） 會完整解除安裝。 下列檔案不會移除的時機**SQLRemoveDriverManager**稱為解除安裝程序的一部分：  
  
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
  
 **SQLRemoveDriverManager**應該先呼叫要遞減的元件使用計數。 **SQLInstallDriverEx**應接著呼叫要遞增的元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的核心元件檔案。 檔案使用方式計數會維持不變，與其他應用程式使用的較舊版本的核心元件檔案現在會使用較新版本的檔案。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
