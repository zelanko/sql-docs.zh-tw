---
description: SQLRemoveDriverManager 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db880d031e803d5778c2af9b2bea08b6ed590e3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499621"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函式
**一致性**  
 引進的版本： ODBC 3.0：已在 Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 及更新版本的作業系統中淘汰。  
  
 **總結**  
 **SQLRemoveDriverManager** 會從系統資訊中的 Odbcinst.ini 專案變更或移除 ODBC 核心元件的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *pdwUsageCount*  
 出在呼叫此函式之後，驅動程式管理員的使用計數。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。 如果在呼叫此函數時，系統資訊中沒有任何專案，則函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriverManager**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除驅動程式管理員資訊，因為它不存在於登錄中或在登錄中找不到。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞減驅動程式管理員的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriverManager** 會補充 **SQLInstallDriverManager** 函式，並更新系統資訊中的元件使用計數。 您只能從安裝應用程式呼叫此函式。  
  
 **SQLRemoveDriverManager** 會將核心元件使用計數遞減1。 如果元件使用計數變成0，則會移除專案系統資訊。 核心元件專案位於系統資訊中的下列位置，標題為 "ODBC Core"：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  當元件使用計數和檔案使用計數達到零時，應用程式不應該實際移除驅動程式管理員檔案。  
  
 **SQLRemoveDriverManager** 並不會實際移除任何檔案。 呼叫程式會負責刪除檔案和維護檔案使用計數。 不過，當元件使用計數和檔案使用計數都已達到零時，不應該移除驅動程式管理員檔案，因為這些檔案可能會被其他尚未遞增檔案使用計數的應用程式使用。  
  
 **SQLRemoveDriverManager** 會在卸載過程中被呼叫。 ODBC 核心元件 (包括驅動程式管理員、資料指標程式庫、安裝程式、語言程式庫、系統管理員、Thunking 檔等等) 都會全部卸載。 在卸載程式中呼叫 **SQLRemoveDriverManager** 時，不會移除下列檔案：  

:::row:::
    :::column:::
        ODBC32DLL  
        ODBCCR32.DLL  
        ODBCCU32.DLL  
        ODBCINT.DLL  
        ODBCTRAC.DLL  
        MSVCRT40.DLL  
        ODBCCP32.CPL  
    :::column-end:::
    :::column:::
        ODBCCP32.DLL  
        ODBC16GT.DLL  
        ODBC32GT.DLL  
        DS16GT.DLL  
        DS32GT.DLL  
        ODBCAD32.EXE  
    :::column-end:::
:::row-end:::

 **SQLRemoveDriverManager** 也會在升級過程中被呼叫。 如果應用程式偵測到它必須執行升級，但先前已安裝驅動程式，則應該移除驅動程式，然後再重新安裝。  
  
 應先呼叫**SQLRemoveDriverManager** ，以遞減元件使用計數。 接著應呼叫**SQLInstallDriverEx** ，以遞增元件的使用計數。 應用程式安裝程式必須將舊的核心元件檔案取代為新的檔案。 檔案使用計數將保持不變，而其他使用較舊版本核心元件檔案的應用程式現在會使用較新的版本檔案。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
