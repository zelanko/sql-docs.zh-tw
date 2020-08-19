---
description: SQLInstallDriverEx 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c200615c9d3bc71ccb146d3b898517611b53eed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421182"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLInstallDriverEx** 會將驅動程式的相關資訊新增至系統資訊中的 Odbcinst.ini 專案，並將驅動程式的 *UsageCount* 增量為1。 但是，如果驅動程式的版本已經存在，但驅動程式的 *UsageCount* 值不存在，則新的 *UsageCount* 值會設定為2。  
  
 此函數不會實際複製任何檔案。 呼叫程式必須負責將驅動程式的檔案正確複製到目標目錄。  
  
 您也可以使用[ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)來存取**SQLInstallDriverEx**的功能。  
  
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
 輸出驅動程式描述通常 (與使用者相關聯的 DBMS 名稱) 呈現給使用者，而不是實體驅動程式名稱。 *LpszDriver*引數必須包含描述驅動程式之成對關鍵字-值組的雙向 null 結束清單。 如需關鍵字值組的詳細資訊，請參閱 [驅動程式規格](../../../odbc/reference/install/driver-specification-subkeys.md)子機碼。 如需有關雙重以 null 終止之字串的詳細資訊，請參閱 [ConfigDSN 函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathIn*  
 輸出安裝之目標目錄的完整路徑，或 null 指標。 如果 *lpszPathIn* 為 null 指標，驅動程式將會安裝在系統目錄中。  
  
 *lpszPathOut*  
 出應安裝驅動程式之目標目錄的路徑。 如果先前未安裝驅動程式， *lpszPathOut* 應該與 *lpszPathIn*相同。 如果先前已安裝驅動程式， *lpszPathOut* 就是先前安裝的路徑。  
  
 *cbPathOutMax*  
 輸出 *LpszPathOut*的長度。  
  
 *pcbPathOut*  
 出 (排除 null 終止字元) 可在 *lpszPathOut*中傳回的總位元組數。 如果可傳回的位元組數目大於或等於 *cbPathOutMax*， *lpszPathOut* 中的輸出路徑會截斷為 *cbPathOutMax* 減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *fRequest*  
 輸出要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_INSTALL_INQUIRY：查詢可以安裝驅動程式的位置。  
  
 ODBC_INSTALL_COMPLETE：完成安裝要求。  
  
 *lpdwUsageCount*  
 出呼叫此函式之後的驅動程式使用計數。  
  
 應用程式不應該設定使用計數。 ODBC 將維持這個計數。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverEx**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|緩衝區長度無效|*LpszPathOut*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathOutMax*引數為0，而*fRequest*是 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszDriver*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|不正確安裝路徑|*LpszPathIn*引數包含不正確路徑。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或翻譯工具安裝程式庫|無法載入驅動程式安裝程式程式庫。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*LpszDriver*引數未包含關鍵字-值組的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞增驅動程式的使用計數。|  
  
## <a name="comments"></a>註解  
 *LpszDriver*引數是以關鍵字/值組形式提供的屬性清單。 每一組都會以 null 位元組終止，而整個清單會以 null 位元組終止。  (也就是兩個 null 位元組標記清單結尾。 ) 這份清單的格式如下所示：  
  
 _驅動程式-desc_ **\\**0Driver **=** _驅動程式-dll-檔案名_ **\\** 0 [安裝 **=** _程式-dll-檔案名_ <b>\\</b> 0]  
  
 [_驅動程式-attr-keyword1_ **=**_value1_ <b>\\</b>0] [_驅動程式-attr-keyword2_ **=** _value2_ <b>\\</b> 0] ... <b>\\</b>0  
  
 其中 \ 0 是 null 位元組，而 *驅動程式-attr-keywordn* 是任何 driver attribute 關鍵字。 關鍵字必須以指定的順序出現。 例如，假設格式化文字檔的驅動程式具有不同的驅動程式和安裝 Dll，而且可以使用副檔名為 .txt 和 .csv 的檔案。 此驅動程式的 *lpszDriver* 引數可能如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假設 SQL Server 的驅動程式沒有個別的安裝 DLL，而且沒有任何驅動程式屬性關鍵字。 此驅動程式的 *lpszDriver* 引數可能如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 在 **SQLInstallDriverEx** 從 *lpszDriver* 引數抓取驅動程式的相關資訊之後，它會將驅動程式描述新增至系統資訊中 Odbcinst.ini 專案的 [ODBC 驅動程式] 區段。 接著，它會建立標題為驅動程式描述的區段，並新增驅動程式 DLL 和安裝程式 DLL 的完整路徑。 最後，它會傳回安裝目標目錄的路徑，但不會將驅動程式檔案複製到其中。 呼叫程式必須實際將驅動程式檔案複製到目標目錄。  
  
 **SQLInstallDriverEx** 會將所安裝驅動程式的元件使用計數遞增1。 如果驅動程式的版本已經存在，但驅動程式的元件使用計數不存在，[新元件使用計數] 值會設定為2。  
  
 應用程式安裝程式會負責實際複製驅動程式檔案，並維護檔案使用計數。 如果之前尚未安裝驅動程式檔案，則應用程式安裝程式必須複製 *lpszPathIn* 路徑中的檔案，並建立檔案使用計數。 如果先前已安裝過檔案，則安裝程式只會遞增檔案使用次數，並在 *lpszPathOut* 引數中傳回先前安裝的路徑。  
  
> [!NOTE]  
>  如需元件使用計數和檔案使用計數的詳細資訊，請參閱 [使用計數](../../../odbc/reference/install/usage-counting.md)。  
  
 如果應用程式先前已安裝較舊版本的驅動程式檔案，則應該將驅動程式卸載後再重新安裝，如此一來，驅動程式元件的使用計數就會是有效的。 必須先呼叫具有 ODBC_REMOVE_DRIVER) 之*fRequest*的**SQLConfigDriver** (，然後再呼叫**SQLRemoveDriver** ，以遞減元件的使用計數。 接著應呼叫**SQLInstallDriverEx**以重新安裝驅動程式，並遞增元件的使用計數。 應用程式安裝程式必須將舊檔案取代為新的檔案。 檔案使用計數會保持不變，而任何其他使用舊版檔案的應用程式現在都會使用較新的版本。  
  
> [!NOTE]  
>  如果先前已安裝驅動程式，並呼叫 **SQLInstallDriverEx** 以在不同的目錄中安裝驅動程式，則此函式會傳回 TRUE，但 *lpszPathOut* 將會包含已安裝驅動程式的目錄。 它不會包含在 *lpszDriver* 引數中輸入的目錄。  
  
 **SQLInstallDriverEx**中*lpszPathOut*的路徑長度允許進行兩階段的安裝程式，因此應用程式可以藉由呼叫*FRequest*為 ODBC_INSTALL_INQUIRY 模式的**SQLInstallDriverEx** ，判斷*cbPathOutMax*應該是什麼。 這會傳回 *pcbPathOut* 緩衝區中可用的位元組總數。 然後，您可以使用 ODBC_INSTALL_COMPLETE 的*fRequest*來呼叫**SQLInstallDriverEx** ，並將*CbPathOutMax*引數設定為*pcbPathOut*緩衝區中的值，再加上 null 終止字元。  
  
 如果您選擇不使用 **SQLInstallDriverEx**的兩階段模型，則必須設定 *cbPathOutMax*，以定義目標目錄路徑的儲存體大小，以及 stdlib.h 中定義的值 _MAX_PATH，以防止截斷。  
  
 當 ODBC_INSTALL_COMPLETE *fRequest* 時， **SQLInstallDriverEx** 不允許 *LpszPathOut* 為 Null (或 *cbPathOutMax* 為 0) 。 如果 *fRequest* 為 ODBC_INSTALL_COMPLETE，當可傳回的位元組數目大於或等於 *cbPathOutMax*時，就會傳回 FALSE，並產生截斷的結果。  
  
 在呼叫 **SQLInstallDriverEx** 之後，應用程式安裝程式已複製驅動程式檔案 (如有必要) ，驅動程式安裝程式 DLL 必須呼叫 **SQLConfigDriver** 來設定驅動程式的設定。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
