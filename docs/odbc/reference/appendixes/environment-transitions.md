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
ms.openlocfilehash: 6b1de2f2147357f9e2ed4f71657b9298c4a13684
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910437"
---
# <a name="environment-transitions"></a>環境轉換
ODBC 環境具有下列三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|E0|未配置的環境|  
|E1|配置的環境，未配置的連接|  
|E2|配置的環境，配置的連接|  
  
 下表顯示每個 ODBC 函數如何影響環境狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(IH)2|E2 [5]<br />HY0107|--[4]|  
|(IH)第|(IH)|--[4]|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 此資料列會顯示*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 時的轉換。  
  
 [4] 以指向有效控制碼的*OutputHandlePtr*呼叫**SQLAllocHandle**會覆寫該控制碼。 這可能是應用程式設計錯誤。  
  
 [5] 已在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [6] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0102|--[1]<br />HY0102|  
  
 [1] 環境上已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 環境上尚未設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)sha-1|--[3]<br />HY0104gb|--[3]<br />HY0104gb|  
|(IH)2|(IH)|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 環境上已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [4] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)sha-1|E0|HY010|  
|(IH)2|(IH)|--[4]<br />E1 [5]|  
|(IH)第|(IH)|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 此資料列會顯示*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 時的轉換。  
  
 [4] 有其他已配置的連接控制碼。  
  
 [5]*句*柄中指定的連接控制碼是唯一配置的連接控制碼。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)sha-1|--|--|  
|(IH)2|(IH)|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當*HandleType*是 SQL_HANDLE_DBC、SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 時，此資料列會顯示轉換。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0102|--|  
  
 [1] 環境上已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 環境上尚未設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />HY0102|HY011|  
  
 [1] 環境上已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 未 SQL_ATTR_ODBC_VERSION*屬性*引數，且環境上尚未設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
