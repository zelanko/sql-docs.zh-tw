---
title: "遠端資料存取的解決方案 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9030af4a02555aac77428ba9490ee72e87b93681
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="solutions-for-remote-data-access"></a>遠端資料存取的解決方案
## <a name="the-issue"></a>問題  
 ADO 可以讓應用程式直接存取和修改資料來源 （有時稱為兩層式系統）。 例如，如果您連接到資料來源，其中包含您的資料，位於直接連接兩層式系統。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 不過，您可以透過如 Microsoft® 網際網路資訊服務 (IIS) 的媒介間接存取資料來源。 這種排列方式通常稱為三層式系統。 IIS 是提供有效率的方式，讓本機或用戶端，叫用跨網際網路或內部網路的遠端或伺服器，程式的應用程式的用戶端/伺服器系統。 伺服器程式取得存取權的資料來源，並選擇性地處理取得的資料。  
  
 比方說，您的內部網路 Web 頁面包含 Microsoft® Visual Basic Scripting Edition (VBScript)，連接到 IIS 中撰寫的應用程式。 IIS 依次連接到實際的資料來源、 擷取資料、 處理以某種方式，和您的應用程式然後傳回已處理的資訊。  
  
 在此範例中，您的應用程式永遠不會直接連接至資料來源;IIS 提供支援。 與 IIS 存取透過 ADO 的資料。  
  
> [!NOTE]
>  不需要根據網際網路或內部網路用戶端/伺服器應用程式 (也就是網頁型)，它可能只組成區域網路上的已編譯程式。 不過，一般的情況下是 Web 應用程式。  
  
 因為某些視覺控制項，例如格線、 核取方塊或清單中，可能會使用傳回的資訊，傳回的資訊必須是容易使用的視覺控制項。  
  
 您想既簡單又有效率的應用程式開發介面支援三層式系統中，並傳回資訊做為輕鬆如同它已擷取的兩層式系統上。 遠端資料服務 (RDS) 是此介面。  
  
## <a name="the-solution"></a>方案  
 RDS 定義程式設計模型，存取和更新資料來源所需的活動序列的 — 存取透過媒介，例如網際網路資訊服務 (IIS) 中的資料。 程式設計模型，摘要說明整個.rds 的功能  
  
## <a name="see-also"></a>另請參閱  
 [基本 RDS 程式設計模型](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



