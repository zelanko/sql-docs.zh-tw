---
title: Microsoft ActiveX Data Objects (ADO) |Microsoft 文件
ms.custom: ''
ms.date: 07/25/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3dda017a73829525f94863302156266beac3797f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO 用於 c + + 程式中，以連接到 SQL Server。 當然，它也可連接到 Azure SQL Database 在雲端中。

本文章中的每個區段描述 ADO 的元件。

> [!NOTE]
> 不同於 ADO 以 ADO.NET 來。 ADO.NET 中，以及許多其他的 SQL 連接驅動程式和其語言，則會開始討論[SQL Server 驅動程式](../connect/sql-connection-libraries.md)。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) 可讓用戶端應用程式來存取及管理從各種來源透過 OLE DB 提供者的資料。 主要的優點是方便使用、 高速低記憶體額外負荷，以及較小的磁碟使用量。 ADO 支援建置用戶端/伺服器和 Web 應用程式的重要功能。  
  
## <a name="ado-md"></a>ADO MD  
 從 Microsoft Visual Basic 和 Microsoft Visual c + + 等語言，Microsoft ActiveX Data Objects （多維度） (ADO MD) 會提供讓您輕鬆存取多維度資料。 ADO MD 可延伸 Microsoft ActiveX Data Objects (ADO) 來包含特定的多維度資料，例如 CubeDef 和資料格集物件的物件。 使用 ADO MD 中，您可以瀏覽多維度結構描述、 查詢 cube 中，並擷取結果。  
  
 ADO 中，例如 ADO MD 會使用基礎的 OLE DB 提供者來存取資料。 若要使用 ADO MD 中，提供者必須是 OLE DB for OLAP 規格所定義的多維度資料提供者 (MDP)。 MDPs 呈現表格式檢視表中而不是表格式資料提供者 (TDPs) 的多維度檢視中的資料有資料。 請參閱您的特定語法和行為，您的提供者所支援的詳細資訊的 OLAP OLE DB 提供者的文件。  
  
## <a name="rds"></a>RDS  
 遠端資料服務 (RDS) 是的 ADO 中，與將資料從伺服器移至用戶端應用程式或 Web 網頁、 管理用戶端上的資料和更新資訊傳回至單一反覆存取伺服器的功能。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX 資料物件的擴充功能資料定義語言和安全性 (ADOX) 是程式設計模型與 ADO 物件的擴充功能。 ADOX 包含物件的結構描述建立和修改，以及安全性。 因為它是以結構描述管理物件為基礎的方法，您可以撰寫程式碼會針對各種資料來源，不論其原生的語法差異。  
  
 ADOX 是核心 ADO 物件的附屬文件庫。 它會公開其他物件的建立、 修改和刪除結構描述物件，例如資料表和程序。 它也維持使用者和群組，並且將授與及撤銷權限物件的安全性物件。  
  
## <a name="documentation"></a>文件集  
 [ADO 安全性設計問題](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程式設計人員指南](../ado/guide/ado-programmer-s-guide.md)  
  
 使用 ADO、 RDS、 ADO MD 和 ADOX 簡介。  
  
 [ADO 程式設計人員參考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 文件的這一節包含每個 ADO、 RDS、 ADO MD 和 ADOX 物件、 集合、 屬性、 動態屬性、 方法、 事件和列舉的主題。  
  
 [ADO 詞彙](../ado/ado-glossary.md)  
  
## <a name="support"></a>支援  
 免費協助 ADO 解決問題，再試一次張貼到 ADO 公用新聞群組。 此新聞群組會監視 Microsoft 產品支援服務 (PSS) 支援專業人員涵蓋 ADO 中，以及其他有經驗的 ADO 開發人員。  
  
 支援選項的進一步資訊可以找到 「 Microsoft 說明及支援網站上。


