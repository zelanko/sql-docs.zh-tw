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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 276b8627588bcd3472c12564db1e8c6e6af1ef2b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212527"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLInstallTranslatorEx**將轉譯器的相關資訊加入至 Odbcinst.ini 區段的 系統資訊 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 轉譯程式登錄機碼）。  
  
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
 [輸入]這必須包含雙向的 null 終止的描述，轉譯器的關鍵字-值配對清單。 如需有關關鍵字-值配對語法的詳細資訊，請參閱[轉譯程式規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **Translator**並**安裝程式**關鍵字必須包含在*lpszTranslator*字串。 轉譯 DLL 會列出**Translator**關鍵字和轉譯程式安裝程式 DLL 列為**安裝**關鍵字。 每個配對會終止具有 NULL 位元組，並將整個清單結尾的 NULL 位元組。 （也就是兩個 NULL 位元組標記清單的結尾）。格式*lpszTranslator*如下所示：  
  
 \0Translator=*translator-DLL 檔名*\0[Setup=*安裝程式-DLL 檔名*\0]\0  
  
 *lpszPathIn*  
 [輸入]轉譯器所要安裝或 null 指標的完整路徑。 如果*lpszPath*為 null 指標，轉譯器將會安裝在系統目錄。  
  
 *lpszPathOut*  
 [輸出]轉譯器應該安裝所在的目標目錄的路徑。 永遠不會安裝此轉譯程式之後，如果*lpszPathOut*等同於*lpszPathIn*。 如果有預先安裝的轉譯器中， *lpszPathOut*是先前安裝的路徑。  
  
 *cbPathOutMax*  
 [輸入]長度*lpszPathOut。*  
  
 *pcbPathOut*  
 [輸出]傳回在可用的位元組總數*lpszPathOut*。 傳回可用的位元組數目是否大於或等於*cbPathOutMax*中的輸出路徑*lpszPathOut*會被截斷成*pcbPathOutMax*減號null 結束字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *常見*  
 [輸入]要求的類型。 *常見*必須包含下列值之一：  
  
 ODBC_INSTALL_INQUIRY:詢問有關轉譯器安裝。  
  
 ODBC_INSTALL_COMPLETE:完成安裝要求。  
  
 *lpdwUsageCount*  
 [輸出]轉譯程式呼叫此函式之後的使用計數。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallTranslatorEx**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszPathOut*引數不是夠大，無法包含的輸出路徑。 緩衝區會包含已截斷的路徑。<br /><br /> *CbPathOutMax*引數為 0，而*常見*引數為 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszTranslator*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|*LpszPathIn*引數包含無效的路徑。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無效的參數順序|*LpszTranslator*引數未包含的關鍵字-值組清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減登錄的元件使用計數|安裝程式無法遞增轉譯程式的使用計數。|  
  
## <a name="comments"></a>註解  
 **SQLInstallTranslatorEx**提供一個機制來安裝，轉譯器。 此函式不會真的複製任何檔案。 呼叫程式會負責將轉譯程式檔案複製。  
  
 **SQLInstallTranslatorEx**已安裝的轉譯器的元件使用計數遞增 1。 如果轉譯程式的版本已經存在，但此轉譯程式的元件使用計數不存在，新元件使用計數的值設定為 2。  
  
 應用程式安裝程式會負責實際將轉譯程式檔案複製和維護的檔案使用計數。 如果轉譯器檔案先前未安裝，應用程式安裝程式必須複製檔案，並建立或多個檔案使用計數。 如果檔案先前已安裝，安裝程式只會增加檔案使用計數。  
  
 如果較舊版本的轉譯程式先前已安裝應用程式中，轉譯器應該解除安裝，然後重新安裝，以便在轉譯程式元件使用計數無效。 **SQLRemoveTranslator**應該呼叫要遞減的元件使用計數，然後**SQLInstallTranslatorEx**應該呼叫要遞增的元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數會維持不變，並使用較舊的版本檔案的其他應用程式現在會使用較新版本。  
  
 在路徑的長度*lpszPathOut*中**SQLInstallTranslatorEx**允許兩階段的安裝程序，因此應用程式可以決定*cbPathOutMax*應該藉由呼叫**SQLInstallTranslatorEx**具有*常見*ODBC_INSTALL_INQUIRY 模式。 這會傳回可用的位元組總數*pcbPathOut*緩衝區。 **SQLInstallTranslatorEx**便可以呼叫具有*常見*ODBC_INSTALL_COMPLETE 的而*cbPathOutMax*引數設定中的值為*pcbPathOut*緩衝區，再加上 null 結束字元。  
  
 如果您選擇不使用的兩階段模型**SQLInstallTranslatorEx**，您必須設定*cbPathOutMax*，做為定義的目標目錄，以值 _MAX_PATH 中，路徑的儲存體的大小定義於 Stdlib.h，以避免截斷。  
  
 當*常見*是 ODBC_INSTALL_COMPLETE， **SQLInstallTranslatorEx**不允許*lpszPathOut*為 NULL (或*cbPathOutMax*若要為 0）。 如果*常見*ODBC_INSTALL_COMPLETE，FALSE 時，會傳回可用來傳回的位元組數字會大於或等於*cbPathOutMax*，這樣會發生截斷。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回的預設轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|選取的轉譯器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|移除轉譯器|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
