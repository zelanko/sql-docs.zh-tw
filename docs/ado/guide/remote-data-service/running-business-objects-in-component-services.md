---
title: "在 元件服務中執行商務物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df0d9faf78e4e63053e96f5513d38a31af0ca827
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="running-business-objects-in-component-services"></a>在 元件服務中執行商務物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 可執行檔 (.exe) 或動態連結程式庫 (.dll)，可以是商務物件。 物件是.dll 或.exe 檔取決於您用來執行的商務物件的組態：  
  
-   可以透過與 DCOM 呼叫商務物件建立為.exe 檔案。 如果透過網際網路資訊服務 (IIS) 時，會使用這些商務物件，因此有額外的資料，將會降低用戶端效能封送處理。  
  
-   透過 IIS，可使用的.dll 檔案所建立的商務物件，因此也會透過 HTTP。 它們也可透過 DCOM 只能透過元件服務，或透過 Microsoft Transaction Server，如果您使用 Windows NT。 商務物件的 Dll 必須在可以透過 IIS 存取它們的 IIS 伺服器電腦上註冊。 有關如何設定 DCOM 上執行的 DLL 的資訊，請參閱 > 一節，[啟用 DCOM 上執行的 DLL](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)。  
  
> [!NOTE]
>  當中介層商務物件會實作為 元件服務 」 元件使用**GetObjectContext**， **SetComplete**，和**SetAbort**，企業物件可以使用元件服務 （或 MTS，如果您使用 Windows NT） 以維護其狀態在多個用戶端呼叫的內容物件。 這個案例是 DCOM，通常會實作之間受信任的用戶端和伺服器在內部使用。 在此情況下， [.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件和[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)交易內容物件來取代用戶端上的方法和**CreateInstance** 所提供的方法**ITransactionContext**介面，並藉由元件服務。  
  
## <a name="see-also"></a>請參閱＜  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


