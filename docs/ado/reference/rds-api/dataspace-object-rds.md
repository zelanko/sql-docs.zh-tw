---
title: '[空間物件（RDS）] |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbd27490e20e8c615ba934299e80f55eb06a5481
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964352"
---
# <a name="dataspace-object-rds"></a>DataSpace 物件 (RDS)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 建立位於仲介層之自訂商務物件的用戶端 proxy。  
  
 遠端資料服務需要商務物件 proxy，才能讓用戶端元件與位於仲介層的商務物件進行通訊。 Proxy 有助於跨進程或電腦界限進行應用程式[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)資料的封裝、unpackaging 和傳輸（封送處理）。  
  
 遠端資料服務使用**RDS。空間**物件的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法，用來建立商務物件 proxy。 每當建立其中介層商務物件的實例時，就會動態建立商務物件 proxy。 遠端資料服務支援下列通訊協定： HTTP、HTTPS （HTTP 安全通訊端）、DCOM 和同進程（用戶端元件和商務物件位於同一部電腦上）。  
  
> [!NOTE]
>  Rds 以「無狀態」的方式運作 **。「空間**」物件使用 HTTP 或 HTTPS 通訊協定。 也就是，在伺服器傳迴響應之後，用戶端要求的任何內部資訊都會遭到捨棄。  
  
> [!NOTE]
>  雖然商務物件在商務物件 proxy 的存留期間似乎存在，但商務物件實際上只會存在，直到回應傳送至要求為止。 發出要求（也就是在商務物件上叫用方法）時，proxy 會開啟與伺服器的新連接，而伺服器則會建立商務物件的新實例。 在商務物件回應要求之後，伺服器會終結商務物件並關閉連接。  
  
> [!NOTE]
>  此行為表示您無法使用商務物件屬性或變數，將資料從一個要求傳遞至另一個。 您必須使用一些其他機制（例如檔案或方法引數）來保存狀態資料。  
  
 RDS 的類別識別碼 **。** 已 BD96C556-65A3-11D0-983A-00C04FC29E36 的空間物件。  
  
 「**空間**」物件可安全地進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [DataSpace 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSpace 物件和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


