---
description: ODBC 概觀
title: ODBC 總覽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13f34a1ef329957854a8b33916b6b29506fc0ad9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421312"
---
# <a name="odbc-overview"></a>ODBC 概觀
Open Database Connectivity (ODBC) 是廣泛接受的應用程式開發介面， (API) 以進行資料庫存取。 它是以呼叫層級介面為基礎， (CLI) 適用于資料庫 Api 的 Open Group 和 ISO/IEC 的規格，並使用結構化查詢語言 (SQL)  (SQL) 作為其資料庫存取語言。  
  
 ODBC 是針對最大的 *互通性* 所設計，也就是單一應用程式存取不同資料庫管理系統的能力， (dbms) 具有相同的原始程式碼。 資料庫應用程式會呼叫 ODBC 介面中的函式，這些函式會在稱為 *驅動程式*的資料庫特定模組中執行。 使用驅動程式會將應用程式與資料庫專屬的呼叫隔離，方式與印表機驅動程式會將文字處理程式與印表機特定的命令隔離。 因為驅動程式會在執行時間載入，所以使用者只需要加入新的驅動程式，就能存取新的 DBMS;不需要重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
