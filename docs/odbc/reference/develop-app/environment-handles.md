---
title: 環境控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300438"
---
# <a name="environment-handles"></a>環境控制代碼
*環境*是用來存取資料的全域內容;與環境相關聯的是本質上的全域資訊，例如：  
  
-   環境的狀態  
  
-   目前的環境層級診斷  
  
-   目前在環境上配置的連接控制碼  
  
-   每個環境屬性的目前設定  
  
 在執行 ODBC （驅動程式管理員或驅動程式）的程式碼片段內，環境控制碼會識別包含此資訊的結構。  
  
 在 ODBC 應用程式中，通常不會使用環境控制碼。 它們一律用於呼叫**SQLDataSources**和**SQLDrivers** ，有時用於對**SQLAllocHandle**、 **SQLEndTran**、 **SQLFreeHandle**、 **SQLGetDiagField**和**SQLGetDiagRec**的呼叫。  
  
 執行 ODBC （驅動程式管理員或驅動程式）的每個程式碼片段都包含一個或多個環境控制碼。 例如，驅動程式管理員會針對連接到它的每個應用程式維護個別的環境控制碼。 環境控制碼會使用**SQLAllocHandle**配置，並與**SQLFreeHandle**一起釋放。
