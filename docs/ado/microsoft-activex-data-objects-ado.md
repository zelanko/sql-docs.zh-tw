---
description: Microsoft ActiveX Data Objects (ADO)
title: Microsoft ActiveX Data Objects (ADO) |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63307b7b0074cca482befd0dfa689684504f26f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451830"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ActiveX Data Objects 是一種程式設計模型，這表示它不會相依于任何指定的後端引擎。 不過，目前唯一支援 ADO 模型的引擎是 OLE DB。 有許多原生 OLE DB 提供者，以及適用于 ODBC 的 OLE DB 提供者。 ADO 是在 c + + 和 Visual Basic 程式中用來連接到 SQL Server 和其他資料庫。 當然，它也適用于連接到雲端中的 Azure SQL Database。

本文中的每一節都將說明 ADO 的元件。

> [!NOTE]
> ADO.NET 與 ADO 不同。 ADO.NET 以及許多其他的 SQL 連接驅動程式和其語言，從 [SQL Server 驅動程式](../connect/sql-connection-libraries.md)開始討論。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) 讓您的用戶端應用程式透過 OLE DB 提供者，存取及管理各種來源的資料。 它的主要優點是容易使用、高速、低記憶體額外負荷，以及小型磁片使用量。 ADO 支援建立用戶端/伺服器和 Web 應用程式的主要功能。  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (多維度)  (ADO MD) 可讓您輕鬆存取來自 Microsoft Visual Basic 和 Microsoft Visual C++ 等語言的多維度資料。 ADO MD 擴充 Microsoft ActiveX Data Objects (ADO) ，以包含多維度資料的特定物件，例如 CubeDef 和資料格集物件。 您可以使用 ADO MD 流覽多維度架構、查詢 cube，以及取得結果。  
  
 如同 ADO，ADO MD 會使用基礎 OLE DB 提供者來取得資料的存取權。 若要使用 ADO MD，提供者必須是由 OLAP 規格 OLE DB 所定義的多維度資料提供者 (MDP) 。 MDPs 在多維度視圖中呈現資料，而不是表格式資料提供者 (TDPs 在表格式視圖中呈現資料的) 。 請參閱 OLAP OLE DB 提供者的檔，以取得提供者所支援之特定語法和行為的詳細資訊。  
  
## <a name="rds"></a>RDS  
 遠端資料服務 (RDS) 是 ADO 的一項功能，可讓您將資料從伺服器移至用戶端應用程式或網頁、操作用戶端上的資料，以及在單一來回行程中將更新傳回伺服器。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至  [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 適用于資料定義語言和安全性 (ADOX) 的 Microsoft ActiveX Data Objects 延伸模組是 ADO 物件和程式設計模型的延伸。 ADOX 包含用於建立和修改架構的物件，以及安全性。 由於它是以物件為基礎的架構操作方法，您可以撰寫程式碼來處理各種不同的資料來源，而不論其原生語法是否有差異。  
  
 ADOX 是核心 ADO 物件的附屬程式庫。 它會公開用於建立、修改和刪除架構物件（例如資料表和程式）的其他物件。 它也包含安全性物件，以維護使用者和群組，以及授與及撤銷物件的許可權。  
  
## <a name="documentation"></a>文件  
 [ADO 安全性設計問題](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程式設計人員指南](../ado/guide/ado-programmer-s-guide.md)  
  
 使用 ADO、RDS、ADO MD 和 ADOX 的簡介。  
  
 [ADO 程式設計人員參考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 檔的這一節包含每個 ADO、RDS、ADO MD 和 ADOX 物件、集合、屬性、動態屬性、方法、事件和列舉的主題。  
  
 [ADO 詞彙](../ado/ado-glossary.md)  
  
## <a name="support"></a>支援  
 如需 ADO 問題的免費說明，請嘗試張貼至 ADO 公用新聞群組。 此新聞群組是由 Microsoft 產品支援服務所監視 (PSS) 支援涵蓋 ADO 的專業人員，以及其他有經驗的 ADO 開發人員。  
  
 關於支援選項的進一步資訊，可於 Microsoft 說明及支援網站中找到。


