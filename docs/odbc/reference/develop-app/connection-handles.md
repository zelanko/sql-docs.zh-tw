---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036435"
---
# <a name="connection-handles"></a>連線控制代碼
*連接*是由驅動程式和資料來源所組成。 連接控制碼會識別每個連接。 連接控制碼不只會定義要使用的驅動程式，而是要與該驅動程式搭配使用的資料來源。 在執行 ODBC （驅動程式管理員或驅動程式）的程式碼區段內，連接控制碼會識別包含連接資訊的結構，如下所示：  
  
-   連接的狀態  
  
-   目前的連接層級診斷  
  
-   目前在連接上配置的語句和描述項的控制碼  
  
-   每個連接屬性的目前設定  
  
 如果驅動程式支援，ODBC 不會防止多個同時連接。 因此，在特定的 ODBC 環境中，多個連接控制碼可能會指向各種不同的驅動程式和資料來源、相同的驅動程式和各種資料來源，或甚至是與相同驅動程式和資料來源的多個連接。 有些驅動程式會限制它們支援的作用中連線數目;**SQLGetInfo**中的 SQL_MAX_DRIVER_CONNECTIONS 選項會指定特定驅動程式支援的作用中連接數目。  
  
 連接控制碼主要用於連接到資料來源（**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**）、從資料來源（**SQLDisconnect**）中斷連接、取得驅動程式和資料來源（**SQLGetInfo**）的相關資訊、抓取診斷（**SQLGetDiagField**和**SQLGetDiagRec**），以及執行交易（**SQLEndTran**）。 當設定並取得連接屬性（**SQLSetConnectAttr**和**SQLGetConnectAttr**）時，以及取得 SQL 語句（**SQLNativeSql**）的原生格式時，也會使用它們。  
  
 連接控制碼會使用**SQLAllocHandle**配置，並與**SQLFreeHandle**一起釋放。
