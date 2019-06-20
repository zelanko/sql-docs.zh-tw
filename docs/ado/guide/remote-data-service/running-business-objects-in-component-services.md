---
title: 在 元件服務中執行商務物件 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: f64909f4f7db1f765d233878631eb90a4760531e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704208"
---
# <a name="running-business-objects-in-component-services"></a>在 Component Services 中執行商務物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 可執行檔 (.exe) 或動態連結程式庫 (.dll)，可以是商務物件。 您用來執行的商務物件的組態取決於該物件是.dll 或.exe 檔案：  
  
-   您可以透過 DCOM 呼叫商務物件建立為.exe 檔案。 如果透過網際網路資訊服務 (IIS) 時，會使用這些商務物件，則會受限於其他封送處理資料，將用戶端效能變慢。  
  
-   透過 IIS 建立，可使用的.dll 檔案所建立的商務物件，因此也會受到 HTTP。 它們也可用 dcom，只能透過元件服務，或透過 Microsoft Transaction Server 中，如果您使用 Windows NT。 商務物件的 Dll 必須透過 IIS 存取 IIS 伺服器電腦上註冊。 如需如何設定在 DCOM 上執行的 DLL 的詳細資訊，請參閱 區段中，[啟用 DLL 以在 DCOM 上執行](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)。  
  
> [!NOTE]
>  當在中間層商務物件會實作為元件服務 」 元件使用**GetObjectContext**， **SetComplete**，並**setabort 回**，企業物件可以使用元件服務 （或 MTS，如果您使用 Windows NT） 以維護其狀態在多個用戶端呼叫的內容物件。 此案例可透過 DCOM，通常會實作之間受信任的用戶端和伺服器的內部網路中。 在此情況下， [rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件和[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)用戶端上的方法會取代交易內容物件並**CreateInstance**方法，它會提供**ITransactionContext**介面，並藉由將元件服務。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


