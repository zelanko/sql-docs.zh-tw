---
title: 標準的程式設計介面 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0e10a6b8c15b6522e6b34ab008295fc411fcd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232067"
---
# <a name="standard-programming-interface"></a>標準程式設計介面
程式設計介面可能是最明顯的候選標準化。 事實上，當開發 ODBC 時，ANSI 和 ISO 已提供標準的內嵌 SQL 和 SQL 模組。 雖然沒有標準存在於資料庫 CLI 中，SQL Access Group-資料庫供應商的產業協會-已考慮是否要建立一個;ODBC 的部分更新版本會成為其工作的基礎。  
  
 適用於 ODBC 的需求之一是單一的應用程式二進位檔必須使用多個 Dbms。 它是基於這個理由，ODBC 不會使用內嵌的 SQL 或模組的語言。 雖然中內嵌的 SQL 和模組語言的語言已標準化，每個繫結至特定 DBMS 的 precompilers。 因此，必須重新編譯應用程式的每個 DBMS 而產生的二進位檔只可搭配單一 DBMS。 雖然這是可接受的迷你電腦和大型主機環境中找到的低容量應用程式，它是無法接受在個人電腦世界裡。 首先，它是邏輯的夢魘，若要將多個版本的高容量的精裝軟體傳遞給客戶;第二，個人電腦的應用程式通常需要同時存取多個 Dbms。  
  
 相反地，實作呼叫層級介面，透過程式庫或位於每個本機; 上的資料庫驅動程式每個 DBMS 需要不同的驅動程式。 現代作業系統可以在執行階段載入這類程式庫 （例如 Microsoft® Windows® 作業系統上的動態連結程式庫），因為單一應用程式可以存取而不必重新編譯的不同 Dbms 資料和也可以存取的資料多個資料庫同時。 隨著新的資料庫驅動程式變得可用，則使用者只可以安裝這些在其電腦上而不必修改、 重新編譯，或重新連結其資料庫應用程式。 此外，會呼叫層級介面是 ODBC 的良好候選項目，因為 Windows-的 ODBC 的原始開發-已進行大量使用這類程式庫的平台。
