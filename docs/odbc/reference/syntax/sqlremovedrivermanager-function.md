---
title: SQL移除驅動程式管理員功能 |微軟文件
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
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301809"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函式
**一致性**  
 介紹的版本:ODBC 3.0:在 Windows XP 服務包 2、Windows 伺服器 2003 服務包 1 和更高版本的操作系統中棄用。  
  
 **摘要**  
 **SQLRemoveDriverManager**更改或刪除系統資訊中的Odbcinst.ini條目中有關ODBC核心元件的資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *pdwUsage( S) Count*  
 【輸出]調用此函數後驅動程式管理器的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。 如果在調用此函數時系統資訊中不存在條目,則函數將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemove 驅動程式管理員**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式*碼值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|註冊表中找不到元件|安裝程式無法刪除驅動程式管理員資訊,因為它要麼不存在在註冊表中,要麼在註冊表中找不到。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減元件使用量計數|安裝程式未能減少驅動程式管理器的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriverManager**補充**SQLInstallDriverManager**功能,並更新系統資訊中的元件使用方式計數。 應僅從設置應用程式調用此功能。  
  
 **SQLRemoveDriverManager**將核心元件使用計數減少 1。 如果元件使用計數為 0,則入口系統資訊將被刪除。 核心元件項目位於系統資訊中的以下位置,標題為「ODBC 核心」:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  當元件使用計數和檔使用計數達到零時,應用程式不應物理刪除驅動程式管理器檔。  
  
 **SQLRemove驅動程式管理員**實際上不會刪除任何檔。 呼叫程式負責刪除檔案和維護檔案使用方式計數。 但是,當元件使用計數和檔使用計數都達到零時,不應刪除驅動程式管理器檔,因為這些檔案可能由未增加檔使用計數的其他應用程式使用。  
  
 **SQLRemoveDriverManager**是作為卸載過程的一部分調用的。 ODBC 核心元件(包括驅動程式管理員、遊標庫、安裝程式、語言庫、管理員、檔等)作為一個整體卸載。 在作為卸載過程的一部分呼叫**SQLRemoveDriverManager**時,不會刪除以下檔:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.Dll|  
|ODBCCR32.Dll|ODBC16GT.Dll|  
|ODBCCU32.Dll|ODBC32GT.Dll|  
|ODBCINT.Dll|DS16GT.Dll|  
|ODBCTRAC。Dll|DS32GT.Dll|  
|MSVCRT40。Dll|ODBCAD32.Exe|  
|ODBCCP32.Cpl||  
  
 **SQLRemoveDriverManager**也稱為升級過程的一部分。 如果應用程式檢測到必須執行升級,並且以前已安裝驅動程式,則應刪除驅動程式,然後重新安裝驅動程式。  
  
 應首先調用**SQLRemoveDriverManager**來減少元件使用計數。 然後應調用**SQLInstallDriverEx**以增加元件使用計數。 應用程式安裝程式必須用新檔替換舊的核心元件檔。 檔案使用方式計數將保持不變,使用舊版本核心元件檔的其他應用程式現在將使用較新版本的檔。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstall 驅動程式管理員](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
