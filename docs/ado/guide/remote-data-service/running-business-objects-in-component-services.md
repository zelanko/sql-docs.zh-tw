---
title: 在元件服務中執行商務物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87eab0ac5611b437f6e0cbe1957a4d6e8652c4b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922272"
---
# <a name="running-business-objects-in-component-services"></a>在 Component Services 中執行商務物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 商務物件可以是可執行檔（.exe）或動態連結程式庫（.dll）。 您用來執行商務物件的設定需視物件是 .dll 或 .exe 檔案而定：  
  
-   以 .exe 檔案建立的商務物件可以透過 DCOM 呼叫。 如果透過 Internet Information Services （IIS）使用這些商務物件，它們會受到額外的資料封送處理，而這會使用戶端效能變慢。  
  
-   建立為 .dll 檔案的商務物件可以透過 IIS 使用，因此也可用於 HTTP。 如果您使用的是 Windows NT，它們也可以透過「元件服務」，或透過 Microsoft 交易伺服器來使用。 商務物件 Dll 必須在 IIS 伺服器電腦上註冊，才能透過 IIS 來存取它們。 如需如何設定 DLL 以在 DCOM 上執行的相關資訊，請參閱[啟用 DLL 以在 dcom 上執行](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)一節。  
  
> [!NOTE]
>  當中介層的商務物件使用**GetObjectCoNtext**、 **SetComplete**和**SetAbort**實作為元件服務元件時，商務物件可以使用元件服務（如果您使用的是 Windows NT）內容物件，就能在多個用戶端呼叫之間維護其狀態。 這種情況可以透過 DCOM 來進行，這通常是在受信任的用戶端與內部網路中的伺服器之間執行。 在此情況下， [RDS。](../../../ado/reference/rds-api/dataspace-object-rds.md)用戶端上的「空間物件」和[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法會由「交易內容物件」和「 **CreateInstance** 」方法（由**ITransactionCoNtext**介面提供並由「元件服務」所執行）取代。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


