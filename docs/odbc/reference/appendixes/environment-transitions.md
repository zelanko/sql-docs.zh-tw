---
title: "環境轉換 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a044161df57f81fee3639fd26c94b5860d5c1913
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="environment-transitions"></a>環境會轉換
ODBC 環境有下列三種狀態。  
  
|State|Description|  
|-----------|-----------------|  
|E0|未配置的環境|  
|E1|配置的環境中，未配置的連接|  
|E2|配置環境中，配置連接|  
  
 下表顯示每個 ODBC 函數如何影響環境狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(KARTRIS)[2]|E2 [5]<br />(HY010)[6]|--[4]|  
|(KARTRIS)[3]|(KARTRIS)|--[4]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 呼叫**SQLAllocHandle**與*OutputHandlePtr*指向有效的控制代碼會覆寫該控制代碼。 這可能是應用程式的程式設計錯誤。  
  
 [已在環境上設定 5] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [6] SQL_ATTR_ODBC_VERSION 環境屬性必須在環境上尚未設定。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [已在環境上設定 1] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 環境屬性必須在環境上尚未設定。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(KARTRIS)[2]|(KARTRIS)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [已在環境上設定 3] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [4] SQL_ATTR_ODBC_VERSION 環境屬性必須在環境上尚未設定。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)[1]|E0|(HY010)|  
|(KARTRIS)[2]|(KARTRIS)|--[4]<br />E1 [5]|  
|(KARTRIS)[3]|(KARTRIS)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 沒有其他配置的連接控制代碼。  
  
 [中指定 5] 的連接控制代碼*處理*已配置的唯一連接控制代碼。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)[1]|--|--|  
|(KARTRIS)[2]|(KARTRIS)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*利用 SQL_HANDLE_DBC、 SQL_HANDLE_STMT，或 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|--[1]<br />(HY010)[2]|--|  
  
 [已在環境上設定 1] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 環境屬性必須在環境上尚未設定。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [已在環境上設定 1] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2]*屬性*引數不是 SQL_ATTR_ODBC_VERSION，而且已不在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="all-other-odbc-functions"></a>其他所有 ODBC 函數  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|(KARTRIS)|--|

