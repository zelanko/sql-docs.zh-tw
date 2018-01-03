---
title: "SQLPostInstallerError 函式 |Microsoft 文件"
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
apiname: SQLPostInstallerError
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLPostInstallerError
helpviewer_keywords: SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1cc79480eb9ef38529612aecb263ee2892a128f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLPostInstallerError**提供機制，讓驅動程式或轉譯程式的安裝程式庫，報告錯誤**ConfigDriver**， **ConfigDSN**，和**ConfigTranslator**函式來安裝程式錯誤佇列。 應用程式不會使用此應用程式開發介面。他們使用**SQLInstallerError**擷取錯誤。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fErrorCode*  
 [輸入]安裝程式錯誤碼。  
  
 *szErrorMsg*  
 [輸入]錯誤訊息文字。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLPostInstallerError**不會將其本身的錯誤值。 如果錯誤成功公佈到安裝程式錯誤佇列 (可以擷取使用**SQLInstallerError**)，會傳回 SQL_SUCCESS。 會傳回 SQL_ERROR，如果中的值*dwErrorCode*引數不是其中一個指定的安裝程式錯誤碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|設定轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
