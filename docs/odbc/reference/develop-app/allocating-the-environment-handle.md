---
title: 配置環境控制碼 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303001"
---
# <a name="allocating-the-environment-handle"></a>配置環境控制代碼
任何 ODBC 應用程式的第一項工作是載入驅動程式管理員;這項作業的執行方式與作業系統相依。 例如，在執行 Microsoft® Windows NT® Server/Windows 2000 Server、Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows®95/98 的電腦上，應用程式會連結到驅動程式管理員程式庫或呼叫**LoadLibrary**來載入驅動程式管理員 DLL。  
  
 下一個工作必須在應用程式可以呼叫任何其他 ODBC 函數之前完成，這是為了初始化 ODBC 環境並配置環境控制碼，如下所示：  
  
1.  應用程式會宣告 SQLHENV 類型的變數。 然後它會呼叫**SQLAllocHandle** ，並傳遞此變數的位址和 SQL_HANDLE_ENV 選項。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存環境相關資訊的結構，並傳回變數中的環境控制碼。  
  
 驅動程式管理員目前不會呼叫驅動程式中的**SQLAllocHandle** ，因為它不知道要呼叫哪一個驅動程式。 在應用程式呼叫函式以連接到資料來源之前，它會延遲在驅動程式中呼叫**SQLAllocHandle** 。 如需詳細資訊，請參閱本節稍後[的連接程式中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 當應用程式使用 ODBC 完成時，它會釋出使用**SQLFreeHandle**的環境控制碼。 釋放環境之後，應用程式設計錯誤就是在 ODBC 函數的呼叫中使用環境的控制碼;這麼做並沒有定義，但可能會產生嚴重的後果。  
  
 呼叫**SQLFreeHandle**時，驅動程式會釋放用來儲存環境相關資訊的結構。 請注意，必須等到已釋放該環境控制碼上的所有連接控制碼之後，才能針對環境控制碼呼叫**SQLFreeHandle** 。  
  
 如需環境控制碼的詳細資訊，請參閱[環境控制碼](../../../odbc/reference/develop-app/environment-handles.md)。
