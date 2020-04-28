---
title: SQLInstallTranslatorEx 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302089"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLInstallTranslatorEx**會將翻譯工具的相關資訊新增至系統資訊的 Odbcinst 區段（HKEY_LOCAL_MACHINE \software\odbc\odbcinst。INI\ODBC 轉譯者登錄機碼）。  
  
 您也可以使用 ODBCCONF 來存取**SQLInstallTranslatorEx**的功能[。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszTranslator*  
 源這必須包含描述翻譯工具之成對關鍵字-值配對的雙向 null 終止清單。 如需有關關鍵字-值組語法的詳細資訊，請參閱[Translator 規格](../../../odbc/reference/install/translator-specification-subkeys.md)子機碼。  
  
 **翻譯工具**和**安裝程式**關鍵字必須包含在*lpszTranslator*字串中。 轉譯 DLL 會與**translator**關鍵字一併列出，而 translator 安裝程式 dll 會與**setup**關鍵字一併列出。 每個配對都會以 Null 位元組結束，而整個清單會以 Null 位元組結束。 （也就是兩個 Null 位元組會標示清單結尾）。*LpszTranslator*的格式如下所示：  
  
 \0Translator =*translator-dll-檔案名*\ 0 [安裝程式 =*安裝程式-dll-filename*\ 0] \ 0  
  
 *lpszPathIn*  
 源要安裝翻譯工具的完整路徑，或 null 指標。 如果*lpszPath*為 null 指標，轉譯者將會安裝在系統目錄中。  
  
 *lpszPathOut*  
 輸出應安裝 translator 的目標目錄路徑。 如果從未安裝過 translator， *lpszPathOut*會與*lpszPathIn*相同。 如果有先前的轉譯器安裝， *lpszPathOut*就是先前安裝的路徑。  
  
 *cbPathOutMax*  
 源LpszPathOut 的長度 *。*  
  
 *pcbPathOut*  
 輸出可用來在*lpszPathOut*中傳回的位元組總數。 如果傳回的位元組數目大於或等於*cbPathOutMax*，則*lpszPathOut*中的輸出路徑會截斷為*pcbPathOutMax*減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *fRequest*  
 源要求的類型。 *fRequest*必須包含下列其中一個值：  
  
 ODBC_INSTALL_INQUIRY：詢問可以安裝 translator 的位置。  
  
 ODBC_INSTALL_COMPLETE：完成安裝要求。  
  
 *lpdwUsageCount*  
 輸出在呼叫此函式之後，翻譯工具的使用計數。  
  
 應用程式不應該設定使用計數。 ODBC 會維護此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallTranslatorEx**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不正確緩衝區長度|*LpszPathOut*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathOutMax*引數為0，且已 ODBC_INSTALL_COMPLETE *fRequest*引數。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszTranslator*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|安裝路徑無效|*LpszPathIn*引數包含不正確路徑。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*LpszTranslator*引數未包含關鍵字-值組的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減登錄的元件使用計數|安裝程式無法遞增 translator 的使用計數。|  
  
## <a name="comments"></a>評價  
 **SQLInstallTranslatorEx**提供只安裝 translator 的機制。 此函式不會實際複製任何檔案。 呼叫程式會負責複製 translator 檔案。  
  
 **SQLInstallTranslatorEx**會將已安裝轉譯器的元件使用量計數增加1。 如果翻譯工具的版本已存在，但翻譯工具的元件使用計數不存在，則新的 [元件使用計數] 值會設為2。  
  
 應用程式安裝程式負責實際複製 translator 檔案和維護檔案使用計數。 如果先前未安裝 translator 檔案，應用程式安裝程式就必須複製該檔案或檔案，並建立檔案或檔案使用計數。 如果先前已安裝檔案，安裝程式只會遞增檔案使用計數。  
  
 如果應用程式先前已安裝較舊版本的翻譯工具，則應該卸載並重新安裝 translator，讓 translator 元件使用計數有效。 應呼叫**SQLRemoveTranslator**以遞減元件使用計數，然後呼叫**SQLInstallTranslatorEx**以遞增元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數會維持不變，而使用較舊版本檔案的其他應用程式現在會使用較新的版本。  
  
 **SQLInstallTranslatorEx**中*lpszPathOut*的路徑長度允許兩階段安裝程式，因此應用程式可以藉由使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*來呼叫**SQLInstallTranslatorEx** ，以判斷*cbPathOutMax*的目標。 這會傳回*pcbPathOut*緩衝區中可用的位元組總數。 然後，可以使用 ODBC_INSTALL_COMPLETE 的*fRequest*和*cbPathOutMax*引數設定為*pcbPathOut*緩衝區中的值，再加上 Null 終止字元，來呼叫**SQLInstallTranslatorEx** 。  
  
 如果您選擇不使用兩階段模型進行**SQLInstallTranslatorEx**，您必須將*cbPathOutMax*（定義目標目錄的儲存空間大小）設定為 _MAX_PATH （如 stdlib.h> 中所定義）的值，以避免截斷。  
  
 當*fRequest*是 ODBC_INSTALL_COMPLETE 時， **SQLInstallTranslatorEx**不允許*LpszPathOut*為 Null （或*cbPathOutMax*為0）。 如果*fRequest*為 ODBC_INSTALL_COMPLETE，當可用的位元組數目大於或等於*cbPathOutMax*時，會傳回 FALSE，結果會發生截斷。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回預設翻譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|選取轉譯者|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|移除轉譯者|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
