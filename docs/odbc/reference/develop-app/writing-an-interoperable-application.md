---
title: "撰寫可互通的應用程式 |Microsoft 文件"
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
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bab5be84b66571f7ca361a3b158921330c00007f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="writing-an-interoperable-application"></a>撰寫可互通的應用程式
每當應用程式使用多個驅動程式針對相同的程式碼，該程式碼必須在這些驅動程式之間的互通。 在大部分情況下，這是容易的工作。 例如，擷取使用順向資料指標的資料列的程式碼也適用於所有的驅動程式。 在某些情況下，這可能會比較困難。 例如，建構 SQL 陳述式中使用的識別項的程式碼需要考慮識別碼案例中，用引號括住，和一段、 兩部分和三部分命名慣例。  
  
 一般情況下，互通性程式碼必須處理增加的功能支援與功能的變化性的問題。 *功能支援*是指是否支援特定功能。 例如，並非所有的 Dbms 支援交易，並可互通的程式碼必須正確運作，不論交易支援。 *功能變化性*指變異受到特定功能的方式。 例如，目錄名稱會放置在某些 Dbms 中的識別項開頭和結尾的其他項目中的識別項。  
  
 在設計階段或執行階段，應用程式可處理功能支援與功能的變化性。 在設計階段處理功能的支援和變化性，開發人員會查看目標 Dbms 和驅動程式，並確保相同的程式碼將會在它們之間的互通。 這通常是在其中具有低或只有有限的互通性的應用程式處理這些問題的方式。  
  
 例如，如果開發人員可保證垂直應用程式將四個特定 Dbms 只能搭配運作，而且每個這些 Dbms 支援交易，應用程式不需要程式碼，以檢查在執行階段的交易支援。 它永遠可以假設交易可用因為設計階段決定應使用只能有四個 Dbms，其中每個支援交易。  
  
 若要在執行階段處理功能的支援和變化性，應用程式必須在執行階段測試不同的功能，並採取適當動作。 這通常是在其中具備高度互通性的應用程式處理這些問題的方式。 功能支援問題，這表示撰寫程式碼，可讓功能選用或撰寫程式碼中未提供模擬功能。 功能變化性問題，這表示撰寫程式碼可支援所有可能變化。  
  
 此章節包含下列主題。  
  
-   [檢查功能的支援和變化](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [監看式的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)

