---
title: "環境控制代碼 |Microsoft 文件"
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
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa388a7724fdda836a9a82b3f00476ed0a4288bf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="environment-handles"></a>環境控制代碼
*環境*是全域內容中的，以存取資料; 相關聯的環境會是全域的本質，例如任何資訊：  
  
-   環境的狀態  
  
-   目前環境層級的診斷  
  
-   目前配置在環境上的連接控制代碼  
  
-   目前設定的每個環境屬性  
  
 在一段程式碼會實作 ODBC （驅動程式管理員或驅動程式），環境控制代碼會識別要包含這項資訊的結構。  
  
 環境控制代碼不會經常使用在 ODBC 應用程式。 永遠用於呼叫**SQLDataSources**和**SQLDrivers**而且有時候用於呼叫**SQLAllocHandle**， **SQLEndTran**，**SQLFreeHandle**， **SQLGetDiagField**，和**SQLGetDiagRec**。  
  
 每個實作 ODBC （驅動程式管理員或驅動程式） 的程式碼片段包含一或多個環境控制代碼。 例如，驅動程式管理員會維護每個應用程式連接到其個別的環境控制代碼。 被配置環境控制代碼**SQLAllocHandle**且已釋放與**SQLFreeHandle**。
