---
title: ODBC 概觀 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ab7586ebc1cd63d028caab0d3c2f09b82c7172
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916073"
---
# <a name="odbc-overview"></a>ODBC 概觀
開放式資料庫連接 (ODBC) 是資料庫存取廣為接受的應用程式開發介面 (API)。 它的 Open Group 和 ISO/IEC 從資料庫 Api 的呼叫層級介面 (CLI) 規格為基礎，並為其資料庫存取語言中使用結構化查詢語言 (SQL)。  
  
 ODBC 針對最大值*互通性*-也就是單一的應用程式存取相同的原始程式碼與不同的資料庫管理系統 (Dbms) 的能力。 資料庫應用程式呼叫函式在 ODBC 介面中，這會在呼叫的特定資料庫的模組中實作*驅動程式*。 使用驅動程式會從資料庫特有呼叫的應用程式隔離的印表機驅動程式隔離印表機特定命令的文字處理程式的方式相同。 因為已在執行階段載入驅動程式，使用者只需要加入新的驅動程式來存取新的 DBMS;您不需要重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
