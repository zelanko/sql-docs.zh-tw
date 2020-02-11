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
ms.openlocfilehash: 673e3e53468780ef261a22b00a2ec1bb9df0e184
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68030600"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLInstallDriverEx**會將驅動程式的相關資訊新增至系統資訊中的 Odbcinst 專案，並將驅動程式的*UsageCount*遞增1。 不過，如果驅動程式的版本已存在，但驅動程式的*UsageCount*值不存在，則新的*UsageCount*值會設為2。  
  
 此函式不會實際複製任何檔案。 呼叫程式會負責正確地將驅動程式的檔案複製到目標目錄。  
  
 您也可以使用 ODBCCONF 來存取**SQLInstallDriverEx**的功能[。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 源呈現給使用者的驅動程式描述（通常是相關聯的 DBMS 名稱），而不是實體驅動程式名稱。 *LpszDriver*引數必須包含描述驅動程式之成對關鍵字-值配對的雙向 null 終止清單。 如需有關關鍵字-值組的詳細資訊，請參閱[驅動程式規格](../../../odbc/reference/install/driver-specification-subkeys.md)子機碼。 如需雙向 null 終止字串的詳細資訊，請參閱[ConfigDSN 函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathIn*  
 源安裝目標目錄的完整路徑，或 null 指標。 如果*lpszPathIn*為 null 指標，驅動程式將會安裝在系統目錄中。  
  
 *lpszPathOut*  
 輸出應安裝驅動程式之目標目錄的路徑。 如果先前未安裝驅動程式， *lpszPathOut*應該與*lpszPathIn*相同。 如果先前已安裝驅動程式， *lpszPathOut*會是先前安裝的路徑。  
  
 *cbPathOutMax*  
 源*LpszPathOut*的長度。  
  
 *pcbPathOut*  
 輸出可在*lpszPathOut*中傳回的位元組總數（不包括 null 終止字元）。 如果傳回的位元組數目大於或等於*cbPathOutMax*，則*lpszPathOut*中的輸出路徑會截斷為*cbPathOutMax*減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *fRequest*  
 源要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_INSTALL_INQUIRY：詢問可以安裝驅動程式的位置。  
  
 ODBC_INSTALL_COMPLETE：完成安裝要求。  
  
 *lpdwUsageCount*  
 輸出在呼叫此函式之後，驅動程式的使用計數。  
  
 應用程式不應該設定使用計數。 ODBC 會維護此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverEx**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不正確緩衝區長度|*LpszPathOut*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathOutMax*引數為0，而*fRequest*為 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszDriver*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|安裝路徑無效|*LpszPathIn*引數包含不正確路徑。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或 translator 安裝程式程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*LpszDriver*引數未包含關鍵字-值組的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用量計數|安裝程式無法增加驅動程式的使用計數。|  
  
## <a name="comments"></a>註解  
 *LpszDriver*引數是成對的屬性清單，其格式為關鍵字-值組。 每個配對都會以 null 位元組結束，而整個清單會以 null 位元組結束。 （也就是兩個 null 位元組會標示清單結尾）。此清單的格式如下所示：  
  
 _驅動程式-desc_ **\\**0Driver**=**_驅動程式-DLL-檔案名_**\\**0**=**[安裝_程式設定-dll-filename_<b>\\</b>0]  
  
 [_驅動程式-attr-keyword1_**=**_value1_<b>\\</b>0][_驅動程式-attr-keyword2_**=**_value2_<b>\\</b>0] .。。<b>\\</b>0  
  
 其中 \ 0 是 null byte，而*驅動程式-attr-keywordn*是任何驅動程式屬性關鍵字。 關鍵字必須以指定的順序出現。 例如，假設格式化文字檔的驅動程式有不同的驅動程式和安裝 Dll，而且可以使用副檔名為 .txt 和 .csv 的檔案。 此驅動程式的*lpszDriver*引數可能如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假設 SQL Server 的驅動程式沒有個別的安裝程式 DLL，而且沒有任何驅動程式屬性關鍵字。 此驅動程式的*lpszDriver*引數可能如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **SQLInstallDriverEx**從*lpszDriver*引數抓取驅動程式的相關資訊之後，它會將驅動程式描述新增至系統資訊中 ODBCINST 專案的 [ODBC 驅動程式] 區段。 接著，它會建立一個標題為的區段，其中包含驅動程式的描述，並新增驅動程式 DLL 和安裝程式 DLL 的完整路徑。 最後，它會傳回安裝的目標目錄路徑，但不會將驅動程式檔案複製到其中。 呼叫程式必須實際將驅動程式檔案複製到目標目錄。  
  
 **SQLInstallDriverEx**會將已安裝驅動程式的元件使用量計數增加1。 如果驅動程式的版本已存在，但驅動程式的元件使用計數不存在，則新的 [元件使用計數] 值會設為2。  
  
 應用程式安裝程式負責實際複製驅動程式檔案和維護檔案使用計數。 如果先前未安裝驅動程式檔案，應用程式安裝程式就必須複製*lpszPathIn*路徑中的檔案，並建立檔案使用計數。 如果先前已安裝檔案，安裝程式只會遞增檔案使用計數，並在*lpszPathOut*引數中傳回先前安裝的路徑。  
  
> [!NOTE]  
>  如需有關元件使用計數和檔案使用計數的詳細資訊，請參閱[使用量計數](../../../odbc/reference/install/usage-counting.md)。  
  
 如果應用程式先前已安裝較舊版本的驅動程式檔案，則應該卸載驅動程式，然後重新安裝，讓驅動程式元件的使用計數有效。 應該先呼叫**SQLConfigDriver** （具有 ODBC_REMOVE_DRIVER 的*fRequest* ），然後再呼叫**SQLRemoveDriver**來遞減元件使用計數。 接著，應呼叫**SQLInstallDriverEx**以重新安裝驅動程式，以遞增元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數會維持不變，而且任何其他使用舊版檔案的應用程式現在都會使用較新的版本。  
  
> [!NOTE]  
>  如果先前已安裝驅動程式，並呼叫**SQLInstallDriverEx**以將驅動程式安裝在不同的目錄中，則此函式會傳回 TRUE，但*lpszPathOut*會包含已安裝驅動程式的目錄。 它不會包含在*lpszDriver*引數中輸入的目錄。  
  
 **SQLInstallDriverEx**中*lpszPathOut*的路徑長度允許兩階段安裝程式，因此應用程式可以藉由使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*來呼叫**SQLInstallDriverEx** ，以判斷*cbPathOutMax*的目標。 這會傳回*pcbPathOut*緩衝區中可用的位元組總數。 然後，可以使用 ODBC_INSTALL_COMPLETE 的*fRequest*和*cbPathOutMax*引數設定為*pcbPathOut*緩衝區中的值，再加上 Null 終止字元，來呼叫**SQLInstallDriverEx** 。  
  
 如果您選擇不使用兩階段模型進行**SQLInstallDriverEx**，您必須將*cbPathOutMax*（定義目標目錄的儲存空間大小）設定為 _MAX_PATH （如 stdlib.h> 中所定義）的值，以避免截斷。  
  
 當*fRequest*是 ODBC_INSTALL_COMPLETE 時， **SQLInstallDriverEx**不允許*LpszPathOut*為 Null （或*cbPathOutMax*為0）。 如果*fRequest*為 ODBC_INSTALL_COMPLETE，當可用的位元組數目大於或等於*cbPathOutMax*時，會傳回 FALSE，結果會發生截斷。  
  
 在呼叫**SQLInstallDriverEx**且應用程式安裝程式已複製驅動程式檔案（如有必要）之後，驅動程式安裝 DLL 必須呼叫**SQLConfigDriver**來設定驅動程式的設定。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
