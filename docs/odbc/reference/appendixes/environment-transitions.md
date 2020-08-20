---
description: 環境轉換
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cb4366a044f42440eb70934b9f853947e4f3224
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466228"
---
# <a name="environment-transitions"></a>環境轉換
ODBC 環境具有下列三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|步進|未配置的環境|  
|E1|配置的環境，未配置的連接|  
|E2|配置的環境，配置的連接|  
  
 下表顯示每個 ODBC 函數如何影響環境狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
| (IH) [2]|E2 [5]<br /> (HY010) [6]|--[4]|  
| (IH) [3]| (IH) |--[4]|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
 [4] 呼叫 **SQLAllocHandle** 時， *OutputHandlePtr* 指向有效的控制碼會覆寫該控制碼。 這可能是應用程式的程式設計錯誤。  
  
 [5] 環境中已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [6] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) |--[1]<br /> (HY010) [2]|--[1]<br /> (HY010) [2]|  
  
 [1] 環境中已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) [1]|--[3]<br /> (HY010) [4]|--[3]<br /> (HY010) [4]|  
| (IH) [2]| (IH) |--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 已在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [4] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) [1]|步進| (HY010) |  
| (IH) [2]| (IH) |--[4]<br />E1 [5]|  
| (IH) [3]| (IH) |--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
 [4] 還有其他配置的連接控制碼。  
  
 [5] *控制碼* 中指定的連接控制碼是唯一配置的連接控制碼。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) [1]|--|--|  
| (IH) [2]| (IH) |--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 *HandleType* 為 SQL_HANDLE_DBC、SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 時，此資料列會顯示轉換。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) |--[1]<br /> (HY010) [2]|--|  
  
 [1] 環境中已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) |--[1]<br /> (HY010) [2]| (HY011) |  
  
 [1] 環境中已設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
 [2] 未 SQL_ATTR_ODBC_VERSION *屬性* 引數，而且尚未在環境上設定 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|步進<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
| (IH) | (IH) |--|
