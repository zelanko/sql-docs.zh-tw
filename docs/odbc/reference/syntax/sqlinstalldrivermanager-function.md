---
title: "SQLInstallDriverManager 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallDriverManager
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallDriverManager
helpviewer_keywords: SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad5ae190d85af4927f1a58808c025d3cebf78b53
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函式
**一致性**  
 版本引入： ODBC 1.0: Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更新版本的作業系統中被取代  
  
 **摘要**  
 **SQLInstallDriverManager**傳回 ODBC 核心元件的安裝的目標目錄的路徑。 呼叫端程式必須實際上將驅動程式管理員的檔案複製到目標目錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszPath*  
 [輸出]安裝的目標目錄的路徑。  
  
 *cbPathMax*  
 [輸入]長度*lpszPath*。 這必須至少是 _MAX_PATH 位元組。  
  
 *pcbPathOut*  
 [輸出]總位元組數 （不含 null 結束位元組） 中傳回*lpszPath*。 如果傳回可用的位元組數目大於或等於*cbPathMax*中的路徑*lpszPath*會被截斷成*cbPathMax*減去 null 結束字元。 *PcbPathOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLInstallDriverManager**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszPath*引數不是大小足以包含 輸出路徑。 緩衝區會包含已截斷的路徑。<br /><br /> *CbPathMax*引數是不超過 _MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞增 ODBC 核心元件使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLInstallDriverManager**呼叫以傳回路徑的 ODBC 核心元件及遞增元件的使用中的系統資訊的計數。 如果驅動程式管理員的版本已經存在，但是驅動程式的元件使用計數不存在，則會將新元件使用計數的值設定為 2。  
  
 應用程式安裝程式會負責實際複製的核心元件的檔案和維護檔案的使用方式計數。 核心元件檔先前未安裝，如果應用程式安裝程式必須複製檔案，並建立檔案使用計數。 如果檔案先前已安裝，安裝程式只是遞增檔案使用計數。  
  
 如果較舊版本的驅動程式管理員先前已安裝應用程式安裝程式，應該解除安裝，然後重新安裝，使有效的核心元件使用計數的核心元件。 **SQLRemoveDriverManager**應該先呼叫元件使用方式計數遞減。 **SQLInstallDriverManager**然後應該呼叫以遞增的元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的核心元件檔案。 檔案使用方式計數將會維持不變，與其他應用程式使用的舊版本的核心元件檔案現在會使用較新版本的檔案。  
  
 在 ODBC 核心元件、 驅動程式，以及轉譯器的全新安裝，應用程式安裝程式應該依序呼叫下列函數： **SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLConfigDriver** (與*常見*ODBC_INSTALL_DRIVER 的)，然後**SQLInstallTranslatorEx**。 中的核心元件、 驅動程式，以及轉譯程式解除安裝，應用程式安裝程式應該依序呼叫下列函數： **SQLRemoveTranslator**， **SQLRemoveDriver**，然後按一下**SQLRemoveDriverManager**。 這些函式必須依照下列順序呼叫。 在所有元件升級時，解除安裝函式應該呼叫序列中，然後安裝函式應該呼叫序列中。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安裝的轉譯器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|移除驅動程式|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|移除驅動程式管理員|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|移除轉譯器|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
