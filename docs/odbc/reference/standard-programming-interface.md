---
title: "標準的程式設計介面 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 235d61849f28b29af7ec0b9ba67fe86b38bf8239
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="standard-programming-interface"></a>標準的程式設計介面
程式設計介面，可能是標準化的最明顯候選項目。 事實上，當開發 ODBC 時，ANSI 和 ISO 已經提供標準的內嵌 SQL 與 SQL 模組。 雖然沒有標準存在於資料庫 CLI，SQL 存取群組 — 資料庫供應商的產業協會 — 已考慮是否要建立一個。組件的 ODBC 稍後變成其工作的基礎。  
  
 其中一個 ODBC 的需求是，必須使用多個 Dbms 二進位單一應用程式。 它是基於這個理由，ODBC 不會使用內嵌的 SQL 或模組的語言。 雖然 SQL 和模組的內嵌語言的語言已標準化，每個繫結至特定 DBMS precompilers。 因此，必須重新編譯應用程式的每個 DBMS，產生的二進位檔只可搭配單一 DBMS。 雖然這是可接受的迷你電腦和大型主機環境中找到的小量應用程式，它是無法接受世界個人電腦。 首先，它是填入對數成長惡夢傳遞多個版本的高容量、 壓縮包裝軟體給客戶。第二，個人電腦應用程式通常需要同時存取多個 Dbms。  
  
 相反地，可以呼叫層級介面實作透過文件庫或位於每個本機電腦; 資料庫驅動程式每個 DBMS 需要不同的驅動程式。 現在的作業系統可以在執行階段載入這類程式庫 （例如 Microsoft® Windows® 作業系統上的動態連結程式庫），因為單一應用程式可以存取不需重新編譯的不同 Dbms 的資料，而且也可以存取的資料多個資料庫同時。 當新的資料庫驅動程式可以使用時，使用者只安裝在其電腦上的這些而不必修改、 重新編譯，或重新連結其資料庫應用程式。 此外，呼叫層級介面已經適合做為 ODBC，因為 Windows — 最初開發 ODBC 的平台-已進行大量使用這類程式庫。

