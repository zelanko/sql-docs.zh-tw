---
title: SQLInstallDriverEx 功能 |微軟文件
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
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302120"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLInstallDriverEx**在系統資訊中將有關驅動程式的資訊添加到 Odbcinst.ini 條目,並將驅動程式的使用*計數*增加 1。 但是,如果驅動程式的版本已存在,但驅動程式的 *「使用方式計數」* 值不存在,則新的 *「使用計數」* 值設定為 2。  
  
 此函數實際上不會複製任何檔。 呼叫程式負責將驅動程式的檔案正確複製到目標目錄。  
  
 **SQLInstallDriverEx**的功能也可以與[ODBCCONF 一起訪問。EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [輸入]向使用者而不是物理驅動程式名稱顯示的驅動程式描述(通常是關聯的 DBMS 的名稱)。 *lpszDriver*參數必須包含描述驅動程式的關鍵字值對的雙 null 終止清單。 有關關鍵字-值對的詳細資訊,請參閱[驅動程式規範子鍵](../../../odbc/reference/install/driver-specification-subkeys.md)。 有關雙空終止字串的詳細資訊,請參閱[ConfigDSN 函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathin*  
 [輸入]安裝的目標目錄的完整路徑或空指標。 如果*lpszPathIn*是空指標,則驅動程式將安裝在系統目錄中。  
  
 *lpszPathOut*  
 【輸出]應安裝驅動程式的目標目錄的路徑。 如果以前未安裝驅動程式,*則 lpszPathOut*應與*lpszPathIn*相同。 如果以前安裝了驅動程式,則*lpszPathOut*是上次安裝的路徑。  
  
 *cbPathOutMax*  
 [輸入]*長度的lpszPathOut。*  
  
 *多巴帕路*  
 【輸出]可用以*lpszPathOut*返回的位元組總數(不包括空終止字元)。 如果可用於返回的位元組數大於或等於*cbPathOutMax,**則 lpszPathOut*中的輸出路徑將截斷為*cbPathOutMax*減去 null 終止字元。 *pcbPathOut*參數可以是空指標。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*參數必須包含以下值之一:  
  
 ODBC_INSTALL_INQUIRY:詢問驅動程式的安裝位置。  
  
 ODBC_INSTALL_COMPLETE:完成安裝請求。  
  
 *lpdwUsage( M) Counts*  
 【輸出]調用此函數後驅動程式的使用計數。  
  
 應用程式不應設置使用計數。 ODBC 將保留此計數。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverEx**返回 FALSE 時,可以通過調用**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszPathOut*參數不夠大,無法包含輸出路徑。 緩衝區包含截斷路徑。<br /><br /> *cbPathOutMax*參數為*0,fRequest*是ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_INSTALL_INQUIRYODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效關鍵字-值對|*lpszDriver*參數包含語法錯誤。|  
|ODBC_ERROR_INVALID_PATH|不合法安裝路徑|*lpszPathIn*參數包含一個無效的路徑。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉換器設定庫|無法載入驅動程式設置庫。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不合法參數序列|*lpszDriver*參數不包含關鍵字-值對的清單。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減元件使用量計數|安裝程式未能增加驅動程式的使用計數。|  
  
## <a name="comments"></a>註解  
 *lpszDriver*參數是關鍵字-值對形式的屬性清單。 每個對都用空位元組終止,整個清單用空位元組終止。 (即,兩個空位元組標記清單的末尾。此清單的格式如下:  
  
 _驅動程式-desc_ **\\****=** 0 驅動程式 _-DLL 檔案名稱_**\\****=** 0[_設定設定-DLL 檔案名_<b>\\</b>0]  
  
 【_驅動程式-attr-關鍵字1_**=**_值1_<b>\\</b>0][_驅動程式-attr-關鍵字2_**=**_值2_<b>\\</b>0]...<b>\\</b>0  
  
 其中 \0 是空位元組,*驅動程式 attr-關鍵字*是任何驅動程式屬性關鍵字。 關鍵字必須按指定順序顯示。 例如,假設格式化文本檔的驅動程式具有單獨的驅動程式並設置 DLL,並且可以使用具有 .txt 和 .csv 擴展名的檔。 此驅動程式的*lpszDriver*參數可能如下所示:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假設 SQL Server 的驅動程式沒有單獨的設置 DLL,並且沒有任何驅動程式屬性關鍵字。 此驅動程式的*lpszDriver*參數可能如下所示:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **SQLInstallDriverEx**從*lpszDriver*參數中檢索有關驅動程式的資訊後,它將驅動程式描述添加到系統資訊中的 Odbcinst.ini 條目的 [ODBC 驅動程式] 部分。 然後,它創建一個標題為驅動程式說明的部分,並添加驅動程式 DLL 和設置 DLL 的完整路徑。 最後,它返回安裝的目標目錄的路徑,但不會將驅動程式檔複製到它。 呼叫程式必須實際將驅動程式檔案複製到目標目錄。  
  
 **SQLInstallDriverEx**將已安裝驅動程式的元件使用量計數增加1。 如果驅動程式的版本已存在,但驅動程式的元件使用計數不存在,則新的元件使用計數值設置為 2。  
  
 應用程式安裝程式負責物理複製驅動程式檔和維護檔案使用方式計數。 如果以前未安裝驅動程式檔,應用程式安裝程式必須在*lpszPathIn*路徑中複製該檔並創建檔使用方式計數。 如果以前已安裝該檔,安裝程式只會增加檔使用方式計數,並在*lpszPathOut*參數中返回先前安裝的路徑。  
  
> [!NOTE]  
>  有關元件使用方式計數和檔案使用方式計數的詳細資訊,請參閱[使用方式計數](../../../odbc/reference/install/usage-counting.md)。  
  
 如果應用程式以前安裝了舊版本的驅動程式檔,則應卸載驅動程式,然後重新安裝驅動程式,以便驅動程式元件使用計數有效。 應首先呼叫**SQLConfigDriver(** 含ODBC_REMOVE_DRIVER*要求*),然後呼叫**SQLRemoveDriver**以減少元件使用計數。 然後應調用**SQLInstallDriverEx**重新安裝驅動程式,從而增加元件使用計數。 應用程式安裝程式必須用新檔取代舊檔。 檔使用方式計數將保持不變,使用舊版本檔的任何其他應用程式現在都將使用較新版本。  
  
> [!NOTE]  
>  如果以前安裝了驅動程式,並且調用**SQLInstallDriverEx**將驅動程式安裝在其他目錄中,則該功能將返回 TRUE,但*lpszPathOut*將包含已安裝驅動程式的目錄。 它將不包括在*lpszDriver*參數中輸入的目錄。  
  
 **SQLInstallDriverEx**中的*lpszPathOut*中的路徑長度允許兩階段安裝過程,因此應用程式可以通過使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*調用**SQLInstallDriverEx**來確定應該是什麼*cbPathOutMax。* 這將返回*pcbPathOut*緩衝區中可用的位元組總數。 然後,可以使用ODBC_INSTALL_COMPLETE *fRequest*和*cbPathOutMax*參數呼叫**sqlInstallDriverEx,** 該參數設定為*pcbPathOut*緩衝區中的值,以及 null 終止字元。  
  
 如果選擇不將雙相模型用於**SQLInstallDriverEx,** 則必須設置*cbPathOutMax*,該模型將目標目錄路徑的儲存大小定義為 stdlib.h 中定義的值_MAX_PATH,以防止截斷。  
  
 當*frequest* ODBC_INSTALL_COMPLETE時 **,SQLInstallDriverEx**不允許*lpszPathOut*為 NULL(或*cbPathOutMax*為 0)。 如果*fRequest*是ODBC_INSTALL_COMPLETE,則當可返回的位元組數大於或等於*cbPathOutMax*時返回 FALSE,結果會出現截斷。  
  
 在調用**SQLInstallDriverEx**並應用程式安裝程式複製驅動程式檔(如有必要)後,驅動程式設置 DLL 必須呼叫**SQLConfigDriver**來設置驅動程式的配置。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝驅動程式管理員|[SQLInstall 驅動程式管理員](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
