---
description: 環境控制代碼
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
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461500"
---
# <a name="environment-handles"></a>環境控制代碼
*環境*是用來存取資料的全域內容;與環境相關聯的任何資訊都是全域性質的資訊，例如：  
  
-   環境的狀態  
  
-   目前的環境層級診斷  
  
-   目前已在環境上配置的連接控制碼  
  
-   每個環境屬性的目前設定  
  
 在處理 ODBC (驅動程式管理員或驅動程式) 的程式碼中，環境控制碼會識別包含這項資訊的結構。  
  
 環境控制碼不常用於 ODBC 應用程式。 它們一律用於呼叫 **SQLDataSources** 和 **SQLDrivers** ，有時會用於 **SQLAllocHandle**、 **SQLEndTran**、 **SQLFreeHandle**、 **SQLGetDiagField**和 **SQLGetDiagRec**的呼叫中。  
  
 在驅動程式管理員或驅動程式) 中執行 ODBC (的每個程式碼都包含一或多個環境控制碼。 例如，驅動程式管理員會為每個連接到它的應用程式維護個別的環境控制碼。 環境控制碼會使用 **SQLAllocHandle** 進行配置，並使用 **SQLFreeHandle**來釋放。
