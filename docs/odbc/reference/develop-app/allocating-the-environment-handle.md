---
description: 配置環境控制代碼
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
ms.openlocfilehash: 390d7f4248d43e6fc6cb7910be5f42cb286f37e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429450"
---
# <a name="allocating-the-environment-handle"></a>配置環境控制代碼
任何 ODBC 應用程式的第一個工作是載入驅動程式管理員;完成此操作的方式與作業系統相依。 例如，在執行 Microsoft® Windows NT® Server/Windows 2000 Server、Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows®95/98 的電腦上，應用程式會連結至驅動程式管理員程式庫，或呼叫 **LoadLibrary** 來載入驅動程式管理員 DLL。  
  
 下一項工作（必須在應用程式可以呼叫任何其他 ODBC 函數之前完成）是初始化 ODBC 環境並配置環境控制碼，如下所示：  
  
1.  應用程式會宣告 SQLHENV 型別的變數。 然後，它會呼叫 **SQLAllocHandle** ，並傳遞這個變數的位址和 SQL_HANDLE_ENV 選項。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存環境相關資訊的結構，並傳回變數中的環境控制碼。  
  
 驅動程式管理員目前不會在驅動程式中呼叫 **SQLAllocHandle** ，因為它不知道要呼叫的驅動程式。 它會延遲在驅動程式中呼叫 **SQLAllocHandle** ，直到應用程式呼叫函式以連接至資料來源。 如需詳細資訊，請參閱本節稍後 [的連接程式中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 當應用程式使用 ODBC 完成時，它會使用 **SQLFreeHandle**釋放環境控制碼。 釋放環境之後，應用程式程式設計錯誤就是在呼叫 ODBC 函數時使用環境的控制碼;這樣做會有未定義但可能會產生嚴重的後果。  
  
 呼叫 **SQLFreeHandle** 時，驅動程式會釋放用來儲存環境相關資訊的結構。 請注意，在釋放該環境控制碼上的所有連接控制碼之前，無法針對環境控制碼呼叫 **SQLFreeHandle** 。  
  
 如需環境控制碼的詳細資訊，請參閱 [環境控制碼](../../../odbc/reference/develop-app/environment-handles.md)。
