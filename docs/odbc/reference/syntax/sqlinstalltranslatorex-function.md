---
description: SQLInstallTranslatorEx 函式
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
ms.openlocfilehash: 7957a04e0dafaeb2177401f775c5cdbb75135569
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421142"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLInstallTranslatorEx** 會將翻譯工具的相關資訊新增至系統資訊 ( # A1\ODBC translator 登錄機碼) 的 Odbcinst.ini 區段。  
  
 您也可以使用[ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)來存取**SQLInstallTranslatorEx**的功能。  
  
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
 輸出這必須包含描述翻譯工具之成對關鍵字-值組的雙向 null 結束清單。 如需關鍵字值組語法的詳細資訊，請參閱 [Translator 規格](../../../odbc/reference/install/translator-specification-subkeys.md)子機碼。  
  
 **翻譯工具**和**安裝程式**關鍵字必須包含在*lpszTranslator*字串中。 轉譯 DLL 是以 **Translator** 關鍵字列出，而且 translator 安裝程式 dll 是以 **setup** 關鍵字列出。 每一組都會以 Null 位元組終止，而整個清單會以 Null 位元組終止。  (也就是兩個 Null 位元組標記清單結尾。 ) *LpszTranslator* 的格式如下所示：  
  
 \0Translator =*translator-DLL-filename*\ 0 [Setup =*setup-dll-filename*\ 0] \ 0  
  
 *lpszPathIn*  
 輸出要安裝 translator 的完整路徑，或 null 指標。 如果 *lpszPath* 為 null 指標，則會在系統目錄中安裝轉譯器。  
  
 *lpszPathOut*  
 出應安裝 translator 的目標目錄路徑。 如果從未安裝過 translator， *lpszPathOut* 就與 *lpszPathIn*相同。 如果有先前的翻譯工具安裝， *lpszPathOut* 就是先前安裝的路徑。  
  
 *cbPathOutMax*  
 輸出LpszPathOut 的長度 *。*  
  
 *pcbPathOut*  
 出可在 *lpszPathOut*中傳回的總位元組數。 如果可傳回的位元組數目大於或等於 *cbPathOutMax*， *lpszPathOut* 中的輸出路徑會截斷為 *pcbPathOutMax* 減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *fRequest*  
 輸出要求的類型。 *fRequest* 必須包含下列其中一個值：  
  
 ODBC_INSTALL_INQUIRY：詢問可安裝 translator 的位置。  
  
 ODBC_INSTALL_COMPLETE：完成安裝要求。  
  
 *lpdwUsageCount*  
 出在呼叫此函式之後，翻譯工具的使用計數。  
  
 應用程式不應該設定使用計數。 ODBC 將維持這個計數。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallTranslatorEx**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|緩衝區長度無效|*LpszPathOut*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathOutMax*引數為0，且已 ODBC_INSTALL_COMPLETE *fRequest*引數。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszTranslator*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|不正確安裝路徑|*LpszPathIn*引數包含不正確路徑。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*LpszTranslator*引數未包含關鍵字-值組的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減登錄的元件使用計數|安裝程式無法遞增 translator 的使用計數。|  
  
## <a name="comments"></a>註解  
 **SQLInstallTranslatorEx** 提供只安裝 translator 的機制。 此函數不會實際複製任何檔案。 呼叫程式會負責複製翻譯工具檔案。  
  
 **SQLInstallTranslatorEx** 會將所安裝轉譯器的元件使用計數遞增1。 如果翻譯工具的版本已經存在，但 translator 的元件使用計數不存在，則新的 [元件使用計數] 值會設定為2。  
  
 應用程式安裝程式會負責實際複製翻譯工具檔案，並維護檔案使用計數。 如果之前尚未安裝 translator 檔案，則應用程式安裝程式必須複製該檔案，然後建立檔案或檔案的使用計數。 如果先前已安裝過檔案，則安裝程式只會遞增檔案使用計數。  
  
 如果應用程式先前已安裝較舊版本的翻譯工具，則應該將轉譯器卸載後再重新安裝，讓 translator 元件的使用計數有效。 應該呼叫**SQLRemoveTranslator**來遞減元件使用計數，然後呼叫**SQLInstallTranslatorEx**以遞增元件的使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數將保持不變，而其他使用舊版檔案的應用程式現在會使用較新版本。  
  
 **SQLInstallTranslatorEx**中*lpszPathOut*的路徑長度允許進行兩階段的安裝程式，因此應用程式可以藉由呼叫*FRequest*為 ODBC_INSTALL_INQUIRY 模式的**SQLInstallTranslatorEx** ，判斷*cbPathOutMax*應該是什麼。 這會傳回 *pcbPathOut* 緩衝區中可用的位元組總數。 然後，您可以使用 ODBC_INSTALL_COMPLETE 的*fRequest*來呼叫**SQLInstallTranslatorEx** ，並將*CbPathOutMax*引數設定為*pcbPathOut*緩衝區中的值，再加上 null 終止字元。  
  
 如果您選擇不使用 **SQLInstallTranslatorEx**的兩階段模型，則必須設定 *cbPathOutMax*，以定義目標目錄路徑的儲存體大小，以及 stdlib.h 中定義的值 _MAX_PATH，以防止截斷。  
  
 當 ODBC_INSTALL_COMPLETE *fRequest* 時， **SQLInstallTranslatorEx** 不允許 *LpszPathOut* 為 Null (或 *cbPathOutMax* 為 0) 。 如果 *fRequest* 為 ODBC_INSTALL_COMPLETE，當可傳回的位元組數目大於或等於 *cbPathOutMax*時，就會傳回 FALSE，並產生截斷的結果。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回預設轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|選取轉譯|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|移除翻譯|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
