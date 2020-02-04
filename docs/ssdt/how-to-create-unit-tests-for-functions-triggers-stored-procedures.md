---
title: 建立針對函式、觸發程序和預存程序的 SQL Server 單元測試
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c7218f035ca907bf9052865408b3a7311e8f75b4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241466"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>HOW TO：建立函式、觸發程序和預存程序的 SQL Server 單元測試

您可以撰寫單元測試來評估任何資料庫物件的變更。 不過，SQL Server Data Tools 包含從 SQL Server [物件總管] 的資料庫專案節點中建立資料庫函式、觸發程序和預存程序測試的額外支援。 Transact\-SQL 程式碼 Stub 可以自動產生，供您自訂。  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>若要從函式、觸發程序或預存程序建立 SQL Server 單元測試  
  
1.  如需加入預存程序的單元測試範例，請參閱[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)中的＜若要建立預存程序的 SQL Server 單元測試＞一節。  
  
    結果不明的測試條件為加入至每一個測試中的預設條件。 包含這個測試條件的目的為要指出尚未實作測試驗證。 當您加入其他測試條件之後，請從測試中刪除這個測試條件。 如需詳細資訊，請參閱[如何：將測試條件加入至 SQL Server 單元測試](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[如何：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
