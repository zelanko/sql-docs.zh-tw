---
description: 遠端資料存取的解決方案
title: 遠端資料存取的解決方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e46994321b73166095acbb0891f5434a6fc86a1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723037"
---
# <a name="solutions-for-remote-data-access"></a>遠端資料存取的解決方案
## <a name="the-issue"></a>問題  
 ADO 可讓您的應用程式直接存取和修改資料來源， (有時稱為兩層系統) 。 例如，如果您的連接是包含資料的資料來源，則這是兩層系統中的直接連接。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
 不過，您可能會想要透過像是 Microsoft® Internet Information Services (IIS) 的媒介，間接存取資料來源。 這種安排有時稱為三層系統。 IIS 是一種用戶端/伺服器系統，可為本機或用戶端應用程式提供有效率的方法，以在整個網際網路或內部網路上叫用遠端或伺服器。 伺服器程式可取得資料來源的存取權，並選擇性地處理取得的資料。  
  
 例如，您的內部網路網頁包含以 Microsoft® Visual Basic Scripting Edition (VBScript) （連接到 IIS）所撰寫的應用程式。 IIS 接著會連接到實際的資料來源、取出資料、以某種方式處理資料，然後將處理過的資訊傳回給您的應用程式。  
  
 在此範例中，您的應用程式永遠不會直接連接到資料來源;IIS 已完成。 和 IIS 透過 ADO 來存取資料。  
  
> [!NOTE]
>  用戶端/伺服器應用程式不一定要以網際網路或內部網路為基礎 (也就是以 Web 為基礎的) -它只能包含在區域網路上的已編譯器。 不過，一般的情況是 Web 應用程式。  
  
 由於某些視覺控制項（例如方格、核取方塊或清單）可能會使用傳回的資訊，因此視覺化控制項必須輕鬆地使用傳回的資訊。  
  
 您需要一個簡單且有效率的應用程式開發介面，可支援三層系統，並以像是在雙層系統上抓取的方式一樣地傳回信息。 遠端資料服務 (RDS) 是這個介面。  
  
## <a name="the-solution"></a>方案  
 RDS 定義了程式設計模型，也就是取得存取及更新資料來源所需的活動順序，以透過媒介取得資料的存取權，例如 Internet Information Services (IIS) 。 程式設計模型會摘要說明 RDS 的整個功能。  
  
## <a name="see-also"></a>另請參閱  
 [基本 RDS 程式設計模型](./basic-rds-programming-model.md)   
 [RDS 案例](./rds-scenario.md)   
 [RDS 教學課程](./rds-tutorial.md)   
 [RDS 使用方式與安全性](./rds-usage-and-security.md)