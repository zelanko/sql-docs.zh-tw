---
title: SQLInstallDriverEx 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ec40b97f8953f114081292ac82069fd4a81692a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132720"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLInstallDriverEx**將驅動程式的相關資訊加入至 Odbcinst.ini 中的項目系統資訊，並遞增駕*UsageCount* 1。 不過，如果新版驅動程式已經存在但*UsageCount*驅動程式不存在，值的新*UsageCount*值設定為 2。  
  
 此函式不會真的複製任何檔案。 它負責呼叫的程式，以正確的驅動程式檔案複製到目標目錄。  
  
 功能**SQLInstallDriverEx**也可以使用存取[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDriver*  
 [輸入]驅動程式描述 （通常是相關聯的 DBMS 的名稱） 呈現給使用者，而不是實體的驅動程式名稱。 *LpszDriver*引數必須包含雙向的 null 終止的關鍵字 / 值組描述驅動程式清單。 如需有關關鍵字 / 值組的詳細資訊，請參閱[驅動程式規格子機碼](../../../odbc/reference/install/driver-specification-subkeys.md)。 如需雙向 null 結尾字串的詳細資訊，請參閱[ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathIn*  
 [輸入]安裝或 null 指標的目標目錄的完整路徑。 如果*lpszPathIn*為 null 指標，驅動程式將會安裝在系統目錄。  
  
 *lpszPathOut*  
 [輸出]安裝驅動程式的目標目錄的路徑。 如果驅動程式先前未安裝， *lpszPathOut*應該是相同*lpszPathIn*。 如果先前已安裝驅動程式， *lpszPathOut*是先前安裝的路徑。  
  
 *cbPathOutMax*  
 [輸入]長度*lpszPathOut*。  
  
 *pcbPathOut*  
 [輸出]（不包括 null 結束字元） 的位元組總數可用以傳回*lpszPathOut*。 傳回可用的位元組數目是否大於或等於*cbPathOutMax*中的輸出路徑*lpszPathOut*會被截斷成*cbPathOutMax*減號null 結束字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *fRequest*  
 [輸入]要求的類型。 *常見*引數必須包含下列值之一：  
  
 ODBC_INSTALL_INQUIRY:查詢驅動程式安裝。  
  
 ODBC_INSTALL_COMPLETE:完成安裝要求。  
  
 *lpdwUsageCount*  
 [輸出]驅動程式在呼叫此函式之後的使用計數。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverEx**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszPathOut*引數不是夠大，無法包含的輸出路徑。 緩衝區會包含已截斷的路徑。<br /><br /> *CbPathOutMax*引數為 0，並*常見*已 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszDriver*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|*LpszPathIn*引數包含無效的路徑。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯器的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無效的參數順序|*LpszDriver*引數未包含的關鍵字-值組清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減的元件使用計數|安裝程式無法遞增驅動程式的使用計數。|  
  
## <a name="comments"></a>註解  
 *LpszDriver*引數是一份關鍵字-值配對的形式的屬性。 每組都終止 null 位元組，並將整個清單結尾 null 位元組。 （也就是兩個 null 位元組標記清單的結尾）。此清單的格式如下所示：  
  
 _driver-desc_ **\\**0Driver**=**_driver-DLL-filename_**\\**0[Setup**=**_setup-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_**=**_value1_<b>\\</b>0][_driver-attr-keyword2_**=**_value2_<b>\\</b>0]...<b>\\</b>0  
  
 \0 所在 null 位元組並*驅動程式-attr-keywordn*任何驅動程式屬性的關鍵字。 關鍵字必須出現在指定的順序。 例如，假設格式化文字檔驅動程式會有不同的驅動程式和安裝程式 Dll，而且可以使用.txt 和.csv 副檔名的檔案。 *LpszDriver*引數，此驅動程式的可能，如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假設 SQL Server 的驅動程式不需要個別的安裝程式 DLL，而且沒有任何驅動程式屬性的關鍵字。 *LpszDriver*引數，此驅動程式的可能，如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 在後**SQLInstallDriverEx**擷取的驅動程式的相關資訊*lpszDriver*引數，它將驅動程式說明加入至 Odbcinst.ini 項目的 [ODBC 驅動程式] 區段上系統中資訊。 然後建立區段標題皆會以驅動程式的描述，並將驅動程式 DLL 的完整路徑，以及安裝程式 DLL。 最後，它會傳回安裝的目標目錄的路徑，但不會將驅動程式檔案複製到它。 呼叫端程式實際上必須將驅動程式檔案複製到目標目錄中。  
  
 **SQLInstallDriverEx**安裝的驅動程式的元件使用計數遞增 1。 如果已存在的驅動程式版本，但驅動程式的元件使用計數不存在，新元件使用計數的值設定為 2。  
  
 應用程式安裝程式會負責實際將驅動程式檔案複製和維護的檔案使用計數。 如果驅動程式檔案先前未安裝，應用程式安裝程式必須將複製的檔案中*lpszPathIn*路徑並建立檔案使用計數。 如果檔案先前已安裝，安裝程式只會遞增檔案使用狀況並傳回先前安裝的路徑*lpszPathOut*引數。  
  
> [!NOTE]  
>  如需有關元件的使用方式計數和檔案的使用方式計數的詳細資訊，請參閱[使用量計算](../../../odbc/reference/install/usage-counting.md)。  
  
 如果先前已將較舊版本的驅動程式檔案安裝應用程式，應該解除安裝驅動程式，並再重新安裝，使驅動程式元件使用計數無效。 **SQLConfigDriver** (使用*常見*ODBC_REMOVE_DRIVER 的)，應該先呼叫，然後**SQLRemoveDriver**應該呼叫要遞減的元件使用計數。 **SQLInstallDriverEx**然後應該呼叫來重新安裝驅動程式，而且要遞增的元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數會維持不變，並使用較舊的版本檔案的任何其他應用程式現在會使用較新版本。  
  
> [!NOTE]  
>  如果先前已安裝驅動程式和**SQLInstallDriverEx**稱為安裝驅動程式在不同的目錄中，此函式會傳回 TRUE，但*lpszPathOut*將 include 目錄其中已安裝驅動程式。 它不會包含在輸入的目錄*lpszDriver*引數。  
  
 在路徑的長度*lpszPathOut*中**SQLInstallDriverEx**允許兩階段的安裝程序，因此應用程式可以決定*cbPathOutMax*應該已經呼叫**SQLInstallDriverEx**具有*常見*ODBC_INSTALL_INQUIRY 模式。 這會傳回可用的位元組總數*pcbPathOut*緩衝區。 **SQLInstallDriverEx**便可以呼叫具有*常見*ODBC_INSTALL_COMPLETE 的而*cbPathOutMax*引數設定中的值為*pcbPathOut*緩衝區，再加上 null 結束字元。  
  
 如果您選擇不使用的兩階段模型**SQLInstallDriverEx**，您必須設定*cbPathOutMax*，做為定義的目標目錄，以值 _MAX_PATH 中，路徑的儲存體的大小定義於 Stdlib.h，以避免截斷。  
  
 當*常見*是 ODBC_INSTALL_COMPLETE， **SQLInstallDriverEx**不允許*lpszPathOut*為 NULL (或*cbPathOutMax*是0)。 如果*常見*ODBC_INSTALL_COMPLETE，FALSE 時，會傳回可用來傳回的位元組數字會大於或等於*cbPathOutMax*，這樣會發生截斷。  
  
 在後**SQLInstallDriverEx**已呼叫和應用程式安裝程式已複製的驅動程式檔案 （如有必要）、 驅動程式安裝程式必須呼叫 DLL **SQLConfigDriver**設定的組態驅動程式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
