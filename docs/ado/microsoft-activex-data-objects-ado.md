---
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
manager: craigg
ms.openlocfilehash: b0994c4ee4c96e5ed9c373ec4bdc94b02ccddff7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156264"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO 會在C++程式來連線到 SQL Server。 當然，它也可以連接到 Azure SQL Database 在雲端中。

這篇文章中的每個區段描述 ADO 的元件。

> [!NOTE]
> ADO.NET 是不同於 ADO。 ADO.NET 和許多其他 SQL 連接驅動程式以及他們的語言，則會開始討論[SQL Server 驅動程式](../connect/sql-connection-libraries.md)。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) 可讓用戶端應用程式存取和處理來自各種來源透過 OLE DB 提供者的資料。 其主要優點是方便使用、 高速、 低記憶體額外負荷，以及較小的磁碟使用量。 ADO 支援建置用戶端/伺服器和 Web 為基礎的應用程式的主要功能。  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects （多維度） (ADO MD) 讓您輕鬆存取多維度資料從語言，例如 Microsoft Visual Basic 和 Microsoft Visual C++。 ADO MD 擴充 Microsoft ActiveX Data Objects (ADO) 來包含專屬於多維度資料，例如 CubeDef 和資料格集物件的物件。 使用 ADO MD 中，您可以瀏覽多維度的結構描述、 查詢 cube，並擷取結果。  
  
 ADO 中，例如 ADO MD 使用基礎的 OLE DB 提供者來存取資料。 若要使用 ADO MD，OLE DB for OLAP 規格所定義的提供者時，必須為多維度資料提供者 (MDP)。 MDPs 表格式檢視中，該有的資料將呈現多維度的檢視，而不是表格式資料提供者 (TDPs) 中的資料。 請參閱您的特定語法和行為，您的提供者所支援的詳細資訊的 OLAP OLE DB 提供者的文件。  
  
## <a name="rds"></a>RDS  
 遠端資料服務 (RDS) 是的 ADO 中，與將資料從伺服器移至用戶端應用程式或 Web 網頁、 操作的用戶端上的資料和更新資訊傳回單一來回行程中的伺服器功能。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX 資料物件的擴充功能資料定義語言和安全性 (ADOX) 是 ADO 物件和程式設計模型的擴充功能。 ADOX 包含物件的結構描述建立和修改，以及安全性。 因為它是以結構描述管理物件為基礎的方法，您可以撰寫程式碼，能針對各種資料來源，不論其原生的語法差異。  
  
 ADOX 是同一系列文件庫到核心 ADO 物件。 它會公開建立、 修改和刪除結構描述物件，例如資料表和程序的其他物件。 它也包含安全性物件，來維持使用者和群組，並授與及撤銷的物件權限。  
  
## <a name="documentation"></a>文件集  
 [ADO 安全性設計問題](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程式設計人員指南](../ado/guide/ado-programmer-s-guide.md)  
  
 簡介如何使用 ADO、 RDS、 ADO MD 和 ADOX。  
  
 [ADO 程式設計人員參考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 文件的本節包含主題中的每一個 ADO、 RDS、 ADO MD 和 ADOX 物件、 集合、 屬性、 動態屬性、 方法、 事件和列舉型別。  
  
 [ADO 詞彙](../ado/ado-glossary.md)  
  
## <a name="support"></a>支援  
 免費協助 ADO 的問題，嘗試張貼至 ADO 公用新聞群組。 Microsoft 產品支援服務 (PSS) 支援專業人員討論 ADO 中，以及其他有經驗的 ADO 開發人員監視此新聞群組。  
  
 Microsoft 說明及支援網站上可支援選項的進一步資訊。


