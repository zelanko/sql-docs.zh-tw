---
title: 環境轉換 |微軟文件
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
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283298"
---
# <a name="environment-transitions"></a>環境轉換
ODBC 環境具有以下三種狀態。  
  
|State|描述|  
|-----------|-----------------|  
|E0|未配置的環境|  
|E1|已配置的環境,未分配的連線|  
|E2|已配置的環境,已分配的連線|  
  
 下表顯示了每個 ODBC 函數如何影響環境狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV時的過渡。  
  
 [2] 此行顯示*HandleType* SQL_HANDLE_DBC時的過渡。  
  
 [3] 此行顯示*HandleType* SQL_HANDLE_STMT或SQL_HANDLE_DESC時的過渡。  
  
 [4] 使用*OutputHandlePtr*調用**SQLAllocHandle,** 指向有效的句柄覆蓋該句柄。 這可能是應用程式程式設計錯誤。  
  
 [5] SQL_ATTR_ODBC_VERSION環境屬性已設置在環境中。  
  
 [6] 未在環境中設置SQL_ATTR_ODBC_VERSION環境屬性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLData 源及 SQL 驅動程式  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] SQL_ATTR_ODBC_VERSION環境屬性已設置在環境中。  
  
 [2] 未在環境中設置SQL_ATTR_ODBC_VERSION環境屬性。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV時的過渡。  
  
 [2] 此行顯示*HandleType* SQL_HANDLE_DBC時的過渡。  
  
 [3] SQL_ATTR_ODBC_VERSION環境屬性已設置在環境中。  
  
 [4] 未在環境中設置SQL_ATTR_ODBC_VERSION環境屬性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV時的過渡。  
  
 [2] 此行顯示*HandleType* SQL_HANDLE_DBC時的過渡。  
  
 [3] 此行顯示*HandleType* SQL_HANDLE_STMT或SQL_HANDLE_DESC時的過渡。  
  
 [4] 還有其他已分配的連接句柄。  
  
 [5]*在句柄*中指定的連接句柄是唯一分配的連接句柄。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 與 SQLGetDiagRec  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV時的過渡。  
  
 [2] 此行顯示*HandleType* SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC時的過渡。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] SQL_ATTR_ODBC_VERSION環境屬性已設置在環境中。  
  
 [2] 未在環境中設置SQL_ATTR_ODBC_VERSION環境屬性。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1] SQL_ATTR_ODBC_VERSION環境屬性已設置在環境中。  
  
 [2]*屬性*參數未SQL_ATTR_ODBC_VERSION,並且未在環境中設置SQL_ATTR_ODBC_VERSION環境屬性。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 功能  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
