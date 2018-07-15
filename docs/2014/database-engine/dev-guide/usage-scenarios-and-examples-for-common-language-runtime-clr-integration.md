---
title: Common Language Runtime (CLR) 整合的使用方式案例和範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
caps.latest.revision: 43
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2f3ecd38a359da8fa7a3042821742493a82073f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326498"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>Common Language Runtime (CLR) 整合的使用案例和範例
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括範例應用程式、封裝範例和許多編碼範例，可用於了解 Common Language Runtime (CLR) 整合的可程式性功能。  
  
 實作這些範例和其他資源的完整 Visual Studio 專案，請瀏覽[Microsoft SQL Server 社群專案和 CodePlex 上的範例](http://go.microsoft.com/fwlink/?LinkID=193935)。  
  
|名稱|描述|  
|----------|-----------------|  
|[從 CLR UDF 存取機器碼](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|示範如何從資料庫內組件中的使用者定義函數來叫用原生 (Unmanaged) C++ 程式碼的函數。|  
|[陣列參數範例](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|示範如何將資訊的陣列從用戶端傳遞至伺服器上的 CLR 整合預存程序，以便在資料庫中建立、更新或刪除資料列集。 這項作業是使用 UDT 來完成。|  
|[日曆感知日期和時間的 UDT 範例](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|定義兩種 UDT，它們提供處理日期和時間的行事曆認知能力。|  
|[CLR 交易範例](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|示範使用位於 System.Transactions 命名空間內的 Managed API 控制交易。|  
|[使用 CLR 及 XML 建立連絡人](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|SQL Server 的「連絡人」範例提供了一些有用的公用程式，以構成基底 AdventureWorks2012 範例資料庫最上層的額外功能層。 第一個公用程式會建立 AdventureWorks2012 資料庫所含各類人員的連絡記錄。 連絡資訊是使用 XML 來指定並傳遞至以 C# 為基礎或 VB 預存程序，以便建立 XML 並將它放入包含此資料庫的正確資料表中。|  
|[貨幣類型及轉換函式](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|使用 C# 語言定義 Currency 使用者定義資料類型。|  
|[使用 CLR 處理大型物件](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|示範在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和檔案系統 (伺服器可使用 CLR 預存程序進行存取) 之間傳送大型二進位物件 (LOB)。|  
|[Hello World Ready 範例](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|示範建立、部署和測試以簡單 World Ready CLR 整合為基礎之預存程序的基本作業。|  
|[Hello World 範例](../../../2014/database-engine/dev-guide/hello-world-sample.md)|示範建立、部署和測試以簡單 CLR 整合為基礎之預存程序的基本作業。|  
|[同處理序資料存取範例](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|包含示範 CLR 同處理序資料存取提供者之各種功能的數個簡單函數。|  
|[結果集範例](../../../2014/database-engine/dev-guide/result-set-sample.md)|示範如何在閱讀查詢結果時執行命令，而不必開啟新連接也不將所有結果讀取到記憶體中。|  
|[傳送資料集範例](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|示範如何在伺服器端以 CLR 為基礎的預存程序內傳回以 ADO.NET 為基礎的資料集，做為用戶端的結果集。|  
|[字串公用程式函式範例](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|包含資料流資料表值函式 (TVF)，以 C# 與 Visual Basic 撰寫，將逗號分隔的字串分割成包含一個資料行的資料表。|  
|[增補感知的字串操作範例](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|顯示可以同時處理 Unicode 和 Surrogate 字元字串的五個增補感知 [!INCLUDE[tsql](../../includes/tsql-md.md)] 字串函數的實作。|  
|[UDT 公用程式](../../../2014/database-engine/dev-guide/udt-utilities.md)|包含數個使用者定義資料類型 (UDT) 公用程式函數。|  
|[未使用的組件清除](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|包含 .NET 預存程序，該預存程序會查詢中繼資料目錄，藉以在目前的資料庫中刪除未使用的組件。|  
|[使用者定義型別](../../../2014/database-engine/dev-guide/user-defined-type.md)|顯示從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和使用 System.Data.SqlClient 的用戶端應用程式建立及使用簡單的 UDT。|  
|[UTF8 字串使用者自訂資料類型&#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|示範 UDT 的實作，即擴充資料庫的類型系統來為 UTF8 編碼值提供儲存體。|  
  
  
