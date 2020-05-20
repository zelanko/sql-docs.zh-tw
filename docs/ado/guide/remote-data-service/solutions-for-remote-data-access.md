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
author: rothja
ms.author: jroth
ms.openlocfilehash: bc2addcc74551e754218f200ae977e6641c214b9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758944"
---
# <a name="solutions-for-remote-data-access"></a>遠端資料存取的解決方案
## <a name="the-issue"></a>問題  
 ADO 可讓您的應用程式直接存取和修改資料來源（有時也稱為兩層式系統）。 例如，如果您的連接是包含資料的資料來源，這就是兩層系統中的直接連接。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 不過，您可能會想要透過媒介（例如 Microsoft® Internet Information Services （IIS））間接存取資料來源。 這種安排有時稱為三層式系統。 IIS 是一種用戶端/伺服器系統，可提供有效率的方式，讓本機或用戶端應用程式在網際網路或內部網路上叫用遠端或伺服器的程式。 伺服器程式可取得資料來源的存取權，並選擇性地處理取得的資料。  
  
 例如，您的內部網路網頁包含以 Microsoft® Visual Basic Scripting Edition （VBScript）撰寫的應用程式，它會連接到 IIS。 IIS 接著會連接到實際的資料來源，抓取資料，以某種方式處理它，然後將處理過的資訊傳回到您的應用程式。  
  
 在此範例中，您的應用程式永遠不會直接連接到資料來源;IIS 已完成。 而且 IIS 會藉由 ADO 來存取資料。  
  
> [!NOTE]
>  用戶端/伺服器應用程式不一定要以網際網路或內部網路為基礎（也就是以 Web 為基礎），它可能只包含區域網路上已編譯的程式。 不過，一般的情況是以 Web 為基礎的應用程式。  
  
 由於某些視覺控制項（例如方格、核取方塊或清單）可能會使用傳回的資訊，因此視覺效果控制項必須很容易使用傳回的資訊。  
  
 您想要一個簡單且有效率的應用程式設計介面，它支援三層式系統，並會如同在兩層式系統上被抓取般般地傳回信息。 遠端資料服務（RDS）是這個介面。  
  
## <a name="the-solution"></a>方案  
 RDS 定義了程式設計模型，這是取得存取和更新資料來源所需的活動順序，以透過媒介（例如 Internet Information Services （IIS））取得資料的存取權。 程式設計模型會摘要說明 RDS 的完整功能。  
  
## <a name="see-also"></a>另請參閱  
 [基本 RDS 程式設計模型](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


