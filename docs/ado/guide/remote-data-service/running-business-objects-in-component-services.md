---
description: 在 Component Services 中執行商務物件
title: 在元件服務中執行商務物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: rothja
ms.author: jroth
ms.openlocfilehash: 4343d8e1bd04d7e8044fa7f3f1b5de6184466d3f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977719"
---
# <a name="running-business-objects-in-component-services"></a>在 Component Services 中執行商務物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 商務物件可以是可執行檔 ( .exe) 或動態連結程式庫 ( .dll) 。 您用來執行商務物件的設定取決於物件是否為 .dll 或 .exe 檔案：  
  
-   建立為 .exe 檔案的商務物件可以透過 DCOM 來呼叫。 如果這些商務物件是透過 Internet Information Services (IIS) 使用，則會受限於額外的資料封送處理，而這會使用戶端效能變慢。  
  
-   建立為 .dll 檔案的商務物件可以透過 IIS 使用，因此也可以透過 HTTP 使用。 如果您使用 Windows NT，也只能透過元件服務或透過 Microsoft Transaction Server 使用它們。 您必須在 IIS 伺服器電腦上註冊商務物件 Dll，才能透過 IIS 來存取它們。 如需有關如何設定 DLL 以在 DCOM 上執行的詳細資訊，請參閱「 [啟用 dll 以在 dcom 上執行](./enabling-a-dll-to-run-on-dcom.md)」一節。  
  
> [!NOTE]
>  使用 **GetObjectCoNtext**、 **SetComplete**和 **SetAbort**將中介層的商務物件實作為元件服務元件時，如果您使用 Windows NT) 內容物件來維持跨多個用戶端呼叫的狀態，則商務物件可以使用元件服務 (或 MTS。 這種情況可以使用 DCOM，這通常是在受信任的用戶端與內部網路中的伺服器之間執行。 在此案例中為[RDS。](../../reference/rds-api/dataspace-object-rds.md)用戶端上的空間物件和[CreateObject](../../reference/rds-api/createobject-method-rds.md)方法會由**ITransactionCoNtext**介面所提供並由元件服務所執行的交易內容物件和**CreateInstance**方法取代。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)