---
title: SQLPostInstallerError 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac7fb545938a0ec5f212e9c0da867fbea5db4817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536618"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLPostInstallerError**提供一個機制來報告錯誤的驅動程式或轉譯程式安裝程式庫**ConfigDriver**， **ConfigDSN**，和**ConfigTranslator**到安裝程式錯誤佇列的函式。 應用程式不會使用此 API 中;它們會使用**SQLInstallerError**擷取錯誤。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fErrorCode*  
 [輸入]安裝程式錯誤碼。  
  
 *szErrorMsg*  
 [輸入]錯誤訊息文字。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLPostInstallerError**本身未公佈錯誤值。 如果錯誤已成功地公佈到安裝程式錯誤佇列 (可擷取使用**SQLInstallerError**)，會傳回 SQL_SUCCESS。 如果，則會傳回 SQL_ERROR 中的值*dwErrorCode*引數不是其中一個指定的安裝程式錯誤代碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|設定轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
