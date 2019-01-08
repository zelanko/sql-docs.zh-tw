---
title: 遠端資料存取的解決方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a761267c3d25619b58f23e2e7b6396f0e9b43958
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535802"
---
# <a name="solutions-for-remote-data-access"></a>遠端資料存取的解決方案
## <a name="the-issue"></a>此問題  
 ADO 可讓您的應用程式來直接存取及修改資料來源 （有時稱為兩層系統）。 比方說，如果您連接到資料來源，其中包含您的資料，位於直接連接兩層式系統。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 不過，您可以透過媒介例如 Microsoft® 網際網路資訊服務 (IIS)，間接地存取資料來源。 這種排列方式通常稱為三層式系統。 IIS 是提供有效率的方式，讓本機或用戶端應用程式叫用透過網際網路或近端內部網路的遠端或伺服器上，程式的用戶端/伺服器系統。 伺服器程式取得存取權的資料來源，並選擇性地處理取得的資料。  
  
 比方說，您的內部網路網頁上包含 Microsoft® Visual Basic Scripting Edition (VBScript)，連接到 IIS 中撰寫的應用程式。 IIS 接著連接到實際的資料來源、 擷取資料、 處理以某種方式，然後傳回您的應用程式的 已處理的資訊。  
  
 在此範例中，您的應用程式永遠不會直接連接至資料來源;IIS 沒有。 與 IIS 存取透過 ADO 的資料。  
  
> [!NOTE]
>  不需要網際網路或近端內部網路為基礎的用戶端/伺服器應用程式 (也就是網頁型)-它可能包含單獨的區域網路上的已編譯程式。 不過，一般的情況下是 Web 應用程式。  
  
 因為某些視覺控制項，例如格線、 核取方塊或清單中，可能會使用傳回的資訊，傳回的資訊必須是容易使用的視覺控制項。  
  
 您想要既簡單又有效率應用程式設計介面，支援三層式系統，並傳回資訊做為輕鬆如同它已擷取兩層式系統上。 遠端資料服務 (RDS) 是此介面。  
  
## <a name="the-solution"></a>方案  
 RDS 定義程式設計模型層的存取和更新資料來源-若要存取透過媒介，例如網際網路資訊服務 (IIS) 中的資料所需的活動序列。 程式設計模型，摘要說明 RDS 的整個功能  
  
## <a name="see-also"></a>另請參閱  
 [基本 RDS 程式設計模型](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


