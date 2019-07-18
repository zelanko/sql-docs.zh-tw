---
title: 配置環境控制代碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 823ea02a2acb6a28f56c58bb40fe684a2589bd24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077177"
---
# <a name="allocating-the-environment-handle"></a>配置環境控制代碼
ODBC 中的任何應用程式的第一個工作是載入驅動程式管理員;如何做到這點與作業系統相關。 比方說，在電腦上執行 Microsoft® Windows NT® Server/Windows 2000 Server、 Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98，應用程式可能是所連結的驅動程式管理員文件庫或呼叫**LoadLibrary**載入驅動程式管理員的 DLL。  
  
 下一步的工作中，應用程式可以呼叫任何其他的 ODBC 函式必須先完成，是初始化 ODBC 環境並配置環境控制代碼，如下所示：  
  
1.  應用程式宣告型別 SQLHENV 的變數。 然後它會呼叫**SQLAllocHandle**並傳遞此變數和 SQL_HANDLE_ENV 選項的位址。 例如:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存環境的相關資訊的結構，並傳回在變數中的環境控制代碼。  
  
 驅動程式管理員不會呼叫**SQLAllocHandle**此驅動程式中的時間，因為它不知道要呼叫哪一個驅動程式。 它會延遲呼叫**SQLAllocHandle**驅動程式，直到應用程式呼叫的函式，來連接到資料來源中。 如需詳細資訊，請參閱 <<c0> [ 在連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)稍後這一節。  
  
 當應用程式完成使用 ODBC 時，它會釋出環境控制代碼**SQLFreeHandle**。 釋放環境，之後應用程式的程式設計錯誤的 ODBC 函式; 呼叫中使用環境的控制代碼如此一來，所以都未定義，但可能嚴重的後果。  
  
 當**SQLFreeHandle**會呼叫結構用來儲存環境的相關資訊的驅動程式版本。 請注意， **SQLFreeHandle**之後已經釋出該環境控制代碼上的所有連接控制代碼無法為環境控制代碼之前呼叫。  
  
 如需有關環境控制代碼的詳細資訊，請參閱[環境處理](../../../odbc/reference/develop-app/environment-handles.md)。
