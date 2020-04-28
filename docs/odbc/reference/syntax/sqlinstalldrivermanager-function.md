---
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
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302109"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函式
**標準**  
 引進的版本： ODBC 1.0：在 Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 和更新版本的作業系統中被取代  
  
 **摘要**  
 **SQLInstallDriverManager**會傳回 ODBC core 元件安裝的目標目錄路徑。 呼叫程式必須實際將驅動程式管理員的檔案複製到目標目錄。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszPath*  
 輸出安裝之目標目錄的路徑。  
  
 *cbPathMax*  
 源*LpszPath*的長度。 這必須至少為 _MAX_PATH 個位元組。  
  
 *pcbPathOut*  
 輸出*LpszPath*中傳回的位元組總數（不包括 null 終止位元組）。 如果傳回的位元組數目大於或等於*cbPathMax*，則*lpszPath*中的路徑會截斷為*cbPathMax*減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverManager**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不正確緩衝區長度|*LpszPath*引數不夠大，無法包含輸出路徑。 緩衝區包含截斷的路徑。<br /><br /> *CbPathMax*引數小於 _MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用量計數|安裝程式無法遞增 ODBC core 元件使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>評價  
 呼叫**SQLInstallDriverManager**以傳回 ODBC 核心元件的路徑，並遞增系統資訊中的元件使用計數。 如果驅動程式管理員的某個版本已存在，但驅動程式的元件使用計數不存在，則新的 [元件使用計數] 值會設為2。  
  
 應用程式安裝程式負責實際複製核心元件檔案，並維護檔案使用計數。 如果先前未安裝核心元件檔案，應用程式安裝程式就必須複製該檔案，並建立檔案使用計數。 如果先前已安裝檔案，安裝程式只會遞增檔案使用計數。  
  
 如果應用程式安裝程式先前已安裝較舊版本的驅動程式管理員，則應卸載核心元件，然後重新安裝，讓核心元件使用計數有效。 應該先呼叫**SQLRemoveDriverManager**以遞減元件使用計數。 接著，應呼叫**SQLInstallDriverManager**來遞增元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的核心元件檔案。 檔案使用計數會維持不變，而使用舊版核心元件檔案的其他應用程式現在會使用較新版本的檔案。  
  
 在全新安裝的 ODBC core 元件、驅動程式和轉譯程式中，應用程式安裝程式應該依序呼叫下列函式： **SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLConfigDriver** （ *fRequest*為 ODBC_INSTALL_DRIVER），然後**SQLInstallTranslatorEx**。 在卸載核心元件、驅動程式和轉譯程式時，應用程式安裝程式應該依序呼叫下列函式： **SQLRemoveTranslator**、 **SQLRemoveDriver**，然後**SQLRemoveDriverManager**。 這些函式必須在此順序中呼叫。 在所有元件的升級中，應依序呼叫所有的卸載函式，然後依序呼叫所有的安裝函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安裝翻譯工具|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|移除驅動程式|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|移除驅動程式管理員|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|移除翻譯工具|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
