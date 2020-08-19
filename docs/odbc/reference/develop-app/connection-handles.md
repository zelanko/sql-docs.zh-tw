---
description: 連線控制代碼
title: 連接控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4457fa72c40892e208057ac013d3da1e557a6d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424790"
---
# <a name="connection-handles"></a>連線控制代碼
*連接*是由驅動程式和資料來源所組成。 連接控制碼會識別每個連接。 連接控制碼不只會定義要使用的驅動程式，也不會定義要與該驅動程式搭配使用的資料來源。 在處理 ODBC (驅動程式管理員或驅動程式) 的程式碼區段內，連接控制碼會識別包含連接資訊的結構，如下所示：  
  
-   連接的狀態  
  
-   目前的連接層級診斷  
  
-   目前在連接上配置之語句和描述項的控制碼  
  
-   每個連接屬性的目前設定  
  
 如果驅動程式支援，ODBC 不會防止多個同時連接。 因此，在特定的 ODBC 環境中，多個連接控制碼可能會指向各種驅動程式和資料來源、相同的驅動程式和各種資料來源，或甚至多個連接至相同的驅動程式和資料來源。 某些驅動程式會限制它們支援的作用中連線數目; **SQLGetInfo** 中的 SQL_MAX_DRIVER_CONNECTIONS 選項會指定特定驅動程式所支援的作用中連線數目。  
  
 連接處理常式主要是在連接至資料來源時使用 (**SQLConnect**、 **SQLDriverConnect**或 **SQLBrowseConnect**) 、從資料來源 (**SQLDisconnect**) 、取得驅動程式和資料來源的相關資訊 (**SQLGetInfo**) 、取得診斷 (**SQLGetDiagField** 和 **SQLGetDiagRec**) ，以及執行 (**SQLEndTran**) 的交易。 當設定和取得連接屬性時，也會使用它們 (**SQLSetConnectAttr** 和 **SQLGetConnectAttr**) ，以及取得 SQL 語句的原生格式 (**SQLNativeSql**) 。  
  
 使用 **SQLAllocHandle** 來配置連接控制碼，並使用 **SQLFreeHandle**來釋放。
