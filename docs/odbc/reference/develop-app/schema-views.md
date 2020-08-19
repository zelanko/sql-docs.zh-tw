---
description: 結構描述檢視
title: 架構視圖 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 34e1b52b5e96b5fedb964e53f14a7b554d12aa05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429070"
---
# <a name="schema-views"></a>結構描述檢視
應用程式可以藉由呼叫 ODBC 目錄函數或使用 INFORMATION_SCHEMA 視圖，從 DBMS 取出中繼資料資訊。 這些視圖是由 ANSI SQL-92 標準所定義。  
  
 如果 DBMS 和驅動程式支援，INFORMATION_SCHEMA views 可提供比 ODBC 目錄函數所提供更強大、更全面的方式來抓取中繼資料。 應用程式可以對這些其中一個視圖執行自己的自訂 **SELECT** 語句、可以聯結 views，或在 views 上執行聯集。 雖然提供更大的公用程式和更廣泛的中繼資料，但 DBMS 通常不支援 INFORMATION_SCHEMA 的視圖。 這可能會隨著更多 Dbms 和驅動程式達成與 SQL-92 的合規性而變更。  
  
 為了判斷支援哪些視圖，應用程式會使用 SQL_INFO_SCHEMA_VIEWS 選項來呼叫 **SQLGetInfo** 。 若要從支援的視圖取出中繼資料，應用程式會執行 **SELECT** 語句，以指定所需的架構資訊。
