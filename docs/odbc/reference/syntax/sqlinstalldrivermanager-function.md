---
title: SQLInstall驅動程式管理員功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302109"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函式
**一致性**  
 介紹的版本:ODBC 1.0:在 Windows XP 服務包 2、Windows 伺服器 2003 服務包 1 和更高版本的作業系統中棄用  
  
 **摘要**  
 **SQLInstallDriverManager**傳回用於安裝 ODBC 核心元件的目標目錄的路徑。 呼叫程式必須實際將驅動程式管理員的檔案複製到目標目錄。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszPath*  
 【輸出]安裝的目標目錄的路徑。  
  
 *cbPathMax*  
 [輸入]*lpszPath*的長度 。 這必須至少為_MAX_PATH位元組。  
  
 *多巴帕路*  
 【輸出]在*lpszPath*中返回的位元組總數(不包括空終止位元組)。 如果可用於返回的位元組數大於或等於*cbPathMax,* 則*lpszPath*中的路徑將被截斷為*cbPathMax*減去空終止字元。 *pcbPathOut*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverManager**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfError 程式*碼值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszPath*參數不夠大,無法包含輸出路徑。 緩衝區包含截斷路徑。<br /><br /> *cbPathMax*參數小於_MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減元件使用量計數|安裝程式未能增加 ODBC 核心元件使用量計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 呼叫**SQLInstallDriverManager**傳回 ODBC 核心元件的路徑,並增加系統資訊中的元件使用計數。 如果驅動程式管理器的版本已存在,但驅動程式的元件使用計數不存在,則新的元件使用計數值設置為 2。  
  
 應用程式安裝程式負責物理複製核心元件檔並維護檔案使用方式計數。 如果以前未安裝核心元件檔,應用程式安裝程式必須複製該檔,並創建檔案使用方式計數。 如果以前已安裝該檔,安裝程式只會增加檔使用方式計數。  
  
 如果應用程式安裝程式以前安裝了舊版本的驅動程式管理器,則應卸載核心元件,然後重新安裝,以便核心元件使用計數有效。 應首先調用**SQLRemoveDriverManager**來減少元件使用計數。 然後應調用**SQLInstallDriverManager**以增加元件使用計數。 應用程式安裝程式必須用新檔替換舊的核心元件檔。 檔案使用方式計數將保持不變,使用舊版本核心元件檔的其他應用程式現在將使用較新版本的檔。  
  
 在重新安裝 ODBC 核心元件、驅動程式和轉換器時,應用程式安裝程式應按順序*fRequest*調用以下函數:SQLInstallDriverManager、SQLInstallDriverEx、SQLConfigDriver(含有ODBC_INSTALL_DRIVER請求),然後**SQLInstallDriverManager**是**SQLInstall 翻譯器Ex。** **SQLInstallDriverEx** **SQLConfigDriver** 在卸載核心元件、驅動程式和轉換器時,應用程式安裝程式應按順序呼叫以下函數 **:SQLRemove 轉換器****、SQLRemoveDriver,** 然後是**SQLRemoveDriverManager**。 這些函數必須按此順序調用。 在升級所有元件時,應按順序調用所有卸載功能,然後按順序調用所有安裝功能。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[SQL 設定驅動程式](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQL安裝驅動程式Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安裝翻譯器|[SQL安裝翻譯器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|移除驅動程式|[SQL 移除驅動程式](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|移除驅動程式管理員|[SQL 移除驅動程式管理員](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|刪除轉換器|[SQL 刪除轉換器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
