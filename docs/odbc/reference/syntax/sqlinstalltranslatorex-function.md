---
title: SQL安裝翻譯器Ex功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302089"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLInstall 翻譯器Ex**將有關轉換器的資訊添加到系統資訊的Odbcinst.ini部分(HKEY_LOCAL_MACHINE_SOFTWARE_ODBC_ODBCINST。INI_ODBC 譯員註冊表項)。  
  
 **SQLInstall 翻譯器Ex**的功能也可以與[ODBCCONF 一起訪問。EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *lpsz 翻譯*  
 [輸入]這必須包含描述轉換器的關鍵字值對的雙空終止清單。 有關關鍵字-值對語法的詳細資訊,請參閱[翻譯器規範子鍵](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **翻譯**器和**安裝程式**關鍵字必須包含在*lpsz 轉換器*字串中。 翻譯 DLL 隨**翻譯者**關鍵字一起列出,翻譯器設定 DLL 隨 **「設定」** 關鍵字一起列出。 每個對都用 NULL 位元組終止,整個清單用 NULL 位元組終止。 (即,兩個 NULL 位元組標記列表的末尾。*lpsz 轉換器*的格式如下:  
  
 {0 轉換器=*翻譯-DLL 檔名*{0}*設定-DLL 檔名*{0}{0}0}0  
  
 *lpszPathin*  
 [輸入]轉換器要安裝位置的完整路徑或空指標。 如果*lpszPath*是空指標,則轉換器將安裝在系統目錄中。  
  
 *lpszPathOut*  
 【輸出]應安裝轉換器的目標目錄的路徑。 如果從未安裝轉換器,*則 lpszPathOut*與*lpszPathIn*相同。 如果之前安裝譯員,*則 lpszPathOut*是先前安裝的路徑。  
  
 *cbPathOutMax*  
 [輸入]*lpszPathOut 的長度。*  
  
 *多巴帕路*  
 【輸出]可在*lpszPathOut*中返回的位元組總數。 如果可用於返回的位元組數大於或等於*cbPathOutMax,**則 lpszPathOut*中的輸出路徑將截斷為*pcbPathOutMax*減去空終止字元。 *pcbPathOut*參數可以是空指標。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*必須包含以下值之一:  
  
 ODBC_INSTALL_INQUIRY:詢問可在哪裡安裝譯員。  
  
 ODBC_INSTALL_COMPLETE:完成安裝請求。  
  
 *lpdwUsage( M) Counts*  
 【輸出]呼叫此函數後轉換器的使用計數。  
  
 應用程式不應設置使用計數。 ODBC 將保留此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstall 翻譯器Ex**返回 FALSE 時,可以通過調用**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszPathOut*參數不夠大,無法包含輸出路徑。 緩衝區包含截斷路徑。<br /><br /> *cbPathOutMax*參數為*0,fRequest*參數為ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_INSTALL_INQUIRYODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效關鍵字-值對|*lpsz 轉換器*參數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|不合法安裝路徑|*lpszPathIn*參數包含一個無效的路徑。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不合法參數序列|*lpsz 轉換器*參數不包含關鍵字-值對的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減註冊表的元件使用量計數|安裝程式未能增加轉換器的使用計數。|  
  
## <a name="comments"></a>註解  
 **SQLInstall 翻譯器Ex**提供了一種僅安裝轉換器的機制。 此函數實際上不會複製任何檔。 呼叫程式負責複製翻譯檔。  
  
 **SQLInstall 轉換器Ex**將已安裝的轉換器的元件使用量計數增加1。 如果已存在轉換器的版本,但譯員的元件使用計數不存在,則新元件使用計數值設置為 2。  
  
 應用程式安裝程式負責物理複製轉換器檔和維護檔案使用方式計數。 如果以前未安裝轉換器檔,應用程式安裝程式必須複製檔案或檔案並創建檔案或檔案使用方式計數。 如果以前已安裝該檔,安裝程式只會增加檔使用方式計數。  
  
 如果應用程式以前安裝了舊版本的轉換器,則應卸載譯員,然後重新安裝,以便譯員元件使用計數有效。 應調用**SQLRemove 轉換器**來遞減元件使用計數,然後調用**SQLInstall 翻譯Ex**以增加元件使用計數。 應用程式安裝程式必須用新檔取代舊檔案或檔。 檔使用方式計數將保持不變,使用舊版本檔的其他應用程式現在將使用較新版本。  
  
 **SQLInstallTranslatorEx**中的*lpszPathOut*中的路徑長度允許兩階段安裝過程,因此應用程式可以通過使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*調用**SQLInstallTranslatorEx**來確定應該是什麼*cbPathOutMax。* 這將返回*pcbPathOut*緩衝區中可用的位元組總數。 然後,可以使用 ODBC_INSTALL_COMPLETE *fRequest*和*cbPathOutMax*參數呼叫**sqlInstallTranslatorEx,** 該參數設定為*pcbPathOut*緩衝區中的值,以及 null 終止字元。  
  
 如果選擇不將雙相模型用於**SQLInstallTranslatorEx,** 則必須設定*cbPathOutMax*,該模型將目標目錄路徑的儲存大小定義為 stdlib.h 中定義的值_MAX_PATH,以防止截斷。  
  
 當*frequest* ODBC_INSTALL_COMPLETE時 **,SQLInstall 翻譯Ex**不允許*lpszPathOut*為 NULL(或*cbPathOutMax*為 0)。 如果*fRequest*是ODBC_INSTALL_COMPLETE,則當可返回的位元組數大於或等於*cbPathOutMax*時返回 FALSE,結果會出現截斷。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回預設翻譯選項|[設定轉換器](../../../odbc/reference/syntax/configtranslator-function.md)|  
|選擇譯員|[SQLGet 轉換器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|刪除譯員|[SQL 刪除轉換器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
