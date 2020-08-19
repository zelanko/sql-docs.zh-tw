---
description: SQLInstallDriverManager 函式
title: SQLInstallDriverManager 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b39e2c9304fd47394617d48f22ac91284af1b45d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421172"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函式
**一致性**  
 引進的版本： ODBC 1.0：已在 Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 及更新版本的作業系統中淘汰  
  
 **總結**  
 **SQLInstallDriverManager** 會傳回安裝 ODBC core 元件之目標目錄的路徑。 呼叫程式必須實際將驅動程式管理員的檔案複製到目標目錄。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszPath*  
 出安裝目標目錄的路徑。  
  
 *cbPathMax*  
 輸出 *LpszPath*的長度。 這至少必須是 _MAX_PATH 個位元組。  
  
 *pcbPathOut*  
 出 (不包括 null 終止位元組的位元組總數) 在 *lpszPath*中傳回。 如果可傳回的位元組數目大於或等於 *cbPathMax*， *lpszPath* 中的路徑會截斷為 *cbPathMax* 減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverManager**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|緩衝區長度無效|*LpszPath*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathMax*引數小於 _MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞增 ODBC 核心元件的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 呼叫**SQLInstallDriverManager**會傳回 ODBC 核心元件的路徑，並在系統資訊中遞增元件的使用計數。 如果驅動程式管理員的版本已經存在，但驅動程式的元件使用計數不存在，[新的元件使用計數] 值會設定為2。  
  
 應用程式安裝程式會負責實際複製核心元件檔案，並維護檔案使用計數。 如果先前未安裝核心元件檔案，則應用程式安裝程式必須複製該檔案，然後建立檔案使用計數。 如果先前已安裝過檔案，則安裝程式只會遞增檔案使用計數。  
  
 如果應用程式安裝程式先前已安裝較舊版本的驅動程式管理員，則應該將核心元件卸載後再重新安裝，如此核心元件的使用計數才會生效。 應先呼叫**SQLRemoveDriverManager** ，以遞減元件使用計數。 接著應呼叫**SQLInstallDriverManager** ，以遞增元件的使用計數。 應用程式安裝程式必須將舊的核心元件檔案取代為新的檔案。 檔案使用計數將保持不變，而其他使用較舊版本核心元件檔案的應用程式現在會使用較新的版本檔案。  
  
 在全新安裝 ODBC core 元件、驅動程式和轉譯程式時，應用程式安裝程式應依序呼叫下列函式： **SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLConfigDriver** (*fRequest* 為 ODBC_INSTALL_DRIVER) ，然後 **SQLInstallTranslatorEx**。 在卸載核心元件、驅動程式和轉譯程式時，應用程式安裝程式應依序呼叫下列函式： **SQLRemoveTranslator**、 **SQLRemoveDriver**和 **SQLRemoveDriverManager**。 這些函數必須在此順序中呼叫。 在所有元件的升級中，都應該依序呼叫所有的卸載函式，然後依序呼叫所有的安裝函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安裝 translator|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|移除驅動程式|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|移除驅動程式管理員|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|移除 translator|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
