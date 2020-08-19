---
description: 標準程式設計介面
title: 標準程式設計介面 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fd0e9e3901ea6b3dcf9a09366b13fe532f1198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448881"
---
# <a name="standard-programming-interface"></a>標準程式設計介面
程式設計介面可能是最明顯的標準化候選。 事實上，在開發 ODBC 時，ANSI 和 ISO 已經提供內嵌 SQL 和 SQL 模組的標準。 雖然資料庫 CLI 沒有任何標準，但是 SQL 存取群組（資料庫供應商的產業協會）是考慮是否要建立一個：ODBC 的元件之後會成為其工作的基礎。  
  
 ODBC 的其中一個需求是，單一應用程式二進位檔必須使用多個 Dbms。 這是因為 ODBC 不會使用內嵌的 SQL 或模組語言。 雖然內嵌 SQL 和模組語言中的語言是標準化的，但每個語言都系結至 DBMS 特定的 precompilers。 因此，必須針對每個 DBMS 重新編譯應用程式，而產生的二進位檔只適用于單一 DBMS。 雖然這對 minicomputer 和大型主機領域中的低容量應用程式來說是可接受的，但個人電腦世界無法接受。 首先，將多個版本的大量、壓縮包裝的軟體傳遞給客戶，是一項物流，其次，個人電腦應用程式通常需要同時存取多個 Dbms。  
  
 另一方面，呼叫層級介面可透過位於每個本機電腦上的程式庫或資料庫驅動程式來執行;每個 DBMS 都需要不同的驅動程式。 由於新式作業系統可以載入這類程式庫 (例如 Microsoft® Windows®作業系統上的動態連結程式庫) 在執行時間，單一應用程式可以從不同的 Dbms 存取資料，而不需要重新編譯，而且也可以同時從多個資料庫存取資料。 當新的資料庫驅動程式可供使用時，使用者可以直接在其電腦上安裝這些驅動程式，而不需要修改、重新編譯或重新連結其資料庫應用程式。 此外，呼叫層級介面是 ODBC 的絕佳候選項，因為 Windows-原本開發 ODBC 的平臺，已廣泛使用此類程式庫。
