---
title: "SQLInstallTranslatorEx 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallTranslatorEx
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallTranslatorEx
helpviewer_keywords: SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 220d3e6b0cc62c2d3d238332975c32e9c38bc030
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLInstallTranslatorEx**將轉譯程式的相關資訊加入至 Odbcinst.ini > 一節的系統資訊 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 轉譯程式登錄機碼）。  
  
 功能**SQLInstallTranslatorEx**也可以使用存取[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]這必須包含雙向的 null 終止的描述轉譯器的關鍵字-值配對清單。 如需關鍵字-值配對語法的詳細資訊，請參閱[轉譯器規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **轉譯程式**和**安裝**關鍵字必須包含在*lpszTranslator*字串。 轉譯 DLL 列為**轉譯程式**關鍵字和轉譯程式安裝 DLL 列為**安裝**關鍵字。 每一對 NULL 位元組，以終止，並將整個清單終止 NULL 位元組。 （也就是兩個 NULL 位元組標記清單的結尾）。格式*lpszTranslator*如下所示：  
  
 \0Translator=*轉譯程式的 DLL 檔名*\0[Setup=*安裝程式-DLL filename*\0]\0  
  
 *lpszPathIn*  
 [輸入]轉譯器所要安裝或 null 指標的完整路徑。 如果*lpszPath*為 null 指標，轉譯器將會安裝在系統目錄。  
  
 *lpszPathOut*  
 [輸出]轉譯器應該安裝所在的目標目錄的路徑。 如果從未安裝的轉譯器， *lpszPathOut*相同*lpszPathIn*。 如果有在先前安裝的轉譯器， *lpszPathOut*是先前安裝的路徑。  
  
 *cbPathOutMax*  
 [輸入]長度*lpszPathOut。*  
  
 *pcbPathOut*  
 [輸出]可用來傳回中的位元組總數*lpszPathOut*。 如果傳回可用的位元組數目大於或等於*cbPathOutMax*中的輸出路徑*lpszPathOut*會被截斷成*pcbPathOutMax*減號null 結束的字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *常見*  
 [輸入]要求的類型。 *常見*必須包含下列值之一：  
  
 ODBC_INSTALL_INQUIRY： 詢問有關安裝的轉譯器的位置。  
  
 ODBC_INSTALL_COMPLETE： 完成安裝要求。  
  
 *lpdwUsageCount*  
 [輸出]轉譯程式呼叫此函式之後使用狀態計數。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護這個計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallTranslatorEx**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszPathOut*引數不是大小足以包含 輸出路徑。 緩衝區會包含已截斷的路徑。<br /><br /> *CbPathOutMax*引數為 0，而*常見*引數以前是 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszTranslator*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|*LpszPathIn*引數包含無效的路徑。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無效的參數順序|*LpszTranslator*引數未包含的關鍵字-值組的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或減少登錄的元件使用計數|安裝程式無法遞增轉譯程式的使用計數。|  
  
## <a name="comments"></a>註解  
 **SQLInstallTranslatorEx**提供一個機制來安裝此轉譯程式。 此函式實際上不會複製任何檔案。 呼叫程式會負責將轉譯程式檔案複製。  
  
 **SQLInstallTranslatorEx**已安裝的轉譯器的元件使用計數遞增 1。 如果轉譯程式的版本已經存在，但元件使用狀態計數的轉譯器不存在，則會將新元件使用計數的值設定為 2。  
  
 應用程式安裝程式會負責實際將轉譯程式檔案複製和維護的檔案使用計數。 如果轉譯程式檔案之前尚未安裝，應用程式安裝程式必須複製的檔案，然後建立或多個檔案使用計數。 如果檔案先前已安裝，安裝程式只會增加檔案使用計數。  
  
 如果較舊版本的轉譯程式先前已安裝應用程式，轉譯器應該解除安裝，然後重新安裝，以便在轉譯程式元件使用計數無效。 **SQLRemoveTranslator**應該呼叫以遞減的元件使用計數，然後**SQLInstallTranslatorEx**應該呼叫來遞增元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數將會維持不變，與其他應用程式使用較舊版本的檔案現在會使用較新版本。  
  
 中的路徑長度*lpszPathOut*中**SQLInstallTranslatorEx**允許兩階段的安裝程序，因此應用程式可以判斷哪些*cbPathOutMax*應該會藉由呼叫**SQLInstallTranslatorEx**與*常見*ODBC_INSTALL_INQUIRY 模式。 這會傳回可用的位元組總數*pcbPathOut*緩衝區。 **SQLInstallTranslatorEx**然後可以使用呼叫*常見*的 ODBC_INSTALL_COMPLETE 和*cbPathOutMax*引數設定中的值為*pcbPathOut*緩衝區，再加上 null 結束字元。  
  
 如果您選擇不使用的兩階段模型**SQLInstallTranslatorEx**，您必須設定*cbPathOutMax*，其定義的目標目錄，以值 _MAX_PATH 中，路徑的儲存體大小為若要避免截斷 Stdlib.h 中定義。  
  
 當*常見*是 ODBC_INSTALL_COMPLETE， **SQLInstallTranslatorEx**不允許*lpszPathOut* null (或*cbPathOutMax*若要為 0）。 如果*常見*ODBC_INSTALL_COMPLETE，FALSE 時，會傳回可用來傳回的位元組數字會大於或等於*cbPathOutMax*，這樣會截斷，就會發生。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回預設轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|選取的轉譯器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|移除轉譯器|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
