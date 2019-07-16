---
title: 環境控制代碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409b2c14282238766457d349287f65d90fe463b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114316"
---
# <a name="environment-handles"></a>環境控制代碼
*環境*是用來存取資料的全域內容，是全球性的本質，例如任何資訊與環境相關聯：  
  
-   環境的狀態  
  
-   目前的環境層級診斷  
  
-   目前環境上配置連接控制代碼  
  
-   目前的設定，每個環境屬性  
  
 在一段程式碼來實作 ODBC （驅動程式管理員或驅動程式），環境控制代碼會識別要包含這項資訊的結構。  
  
 環境控制代碼不會經常使用在 ODBC 應用程式。 一律會對呼叫中使用**SQLDataSources**並**SQLDrivers**有時用於呼叫**SQLAllocHandle**， **SQLEndTran**，**SQLFreeHandle**， **SQLGetDiagField**，並**SQLGetDiagRec**。  
  
 每一段程式碼來實作 ODBC （驅動程式管理員或驅動程式） 包含一或多個環境控制代碼。 例如，驅動程式管理員會維護已連線到它的每個應用程式的不同的環境控制代碼。 被配置環境控制代碼**SQLAllocHandle**和與釋放**SQLFreeHandle**。
