---
title: 架構檢視 |微軟文件
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
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304249"
---
# <a name="schema-views"></a>結構描述檢視
應用程式可以通過調用 ODBC 目錄函數或使用INFORMATION_SCHEMA檢視從 DBMS 檢索元數據資訊。 視圖由 ANSI SQL-92 標準定義。  
  
 如果 DBMS 和驅動程式支援,INFORMATION_SCHEMA檢視提供了比 ODBC 目錄函數提供的更強大、更全面的檢索元數據的方法。 應用程式可以針對這些檢視之一執行其自己的自定義**SELECT**語句,可以聯接視圖,也可以對視圖執行聯合。 雖然提供更大的實用程式和更廣泛的元數據,但 DBMS 通常不支援INFORMATION_SCHEMA檢視。 隨著更多 DBMS 和驅動程式符合 SQL-92,這種情況可能會發生變化。  
  
 要確定哪些檢視受支援,應用程式使用SQL_INFO_SCHEMA_VIEWS選項調用**SQLGetInfo。** 若要從受支援的檢視圖圖圖圖,應用程式將執行**SELECT**語句,指定所需的架構資訊。
