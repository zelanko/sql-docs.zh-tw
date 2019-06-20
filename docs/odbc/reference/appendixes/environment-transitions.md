---
title: 環境轉換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ed2bbf40ac333db34d3920b2ed2ec688c344bfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63189002"
---
# <a name="environment-transitions"></a>環境轉換
ODBC 環境會有下列三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|E0|未配置的環境|  
|E1|配置的環境中，未配置的連接|  
|E2|配置環境中，配置連接|  
  
 下表顯示每個 ODBC 函數如何影響環境的狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 呼叫**SQLAllocHandle**具有*OutputHandlePtr*指向有效的控制代碼會覆寫該控制代碼。 這可能是應用程式的程式設計錯誤。  
  
 [已在環境上設定 5] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [不在環境上已設定 6] SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] SQL_ATTR_ODBC_VERSION 環境屬性已設定的環境。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 環境屬性具有尚未設定的環境。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [已在環境上設定 3] 的 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [4] SQL_ATTR_ODBC_VERSION 環境屬性具有尚未設定的環境。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 時發生其他配置的連接控制代碼。  
  
 [5] 中指定的連接控制代碼*處理*是唯一的配置的連接控制代碼。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*是利用 SQL_HANDLE_DBC、 SQL_HANDLE_STMT，還是 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] SQL_ATTR_ODBC_VERSION 環境屬性已設定的環境。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 環境屬性具有尚未設定的環境。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1] SQL_ATTR_ODBC_VERSION 環境屬性已設定的環境。  
  
 [2]*屬性*引數不 SQL_ATTR_ODBC_VERSION，而且有尚未 SQL_ATTR_ODBC_VERSION 環境屬性設定的環境。  
  
## <a name="all-other-odbc-functions"></a>所有其他的 ODBC 函數  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
