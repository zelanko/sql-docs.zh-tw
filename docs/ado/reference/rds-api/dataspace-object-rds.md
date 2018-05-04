---
title: 資料空間物件 (RDS) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed1ff8e4f9cff153718fa1ccae78a3565183c707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="dataspace-object-rds"></a>資料空間物件 (RDS)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 建立自訂商務物件位於中介層上的用戶端 proxy。  
  
 遠端資料服務需要商務物件 proxy，以便用戶端元件可以與位於中介層商務物件通訊。 Proxy 促進封裝、 unpackaging，和傳輸 （封送處理） 的應用程式的[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)跨處理序或電腦界限的資料。  
  
 遠端資料服務會使用 **.RDSDataSpace**物件的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法來建立商務物件的 proxy。 每當建立中介層商務物件與對應的執行個體時，動態建立的商務物件的 proxy。 遠端資料服務支援下列通訊協定： HTTP、 HTTPS （HTTP 安全通訊端）、 DCOM 和同處理序 （用戶端元件和商務物件位於同一部電腦上）。  
  
> [!NOTE]
>  RDS 行為 「 無狀態 」 的方式時 **.RDSDataSpace**物件使用的 HTTP 或 HTTPS 通訊協定。 亦即，伺服器會傳回回應之後，會捨棄任何有關用戶端要求的內部資訊。  
  
> [!NOTE]
>  雖然商務物件的存留期間的商務物件 proxy 存在，商務物件確實存在才傳送回應至要求。 要求發出時 （也就是一種方法會叫用商務物件上），proxy 會開啟新的連接到伺服器並伺服器建立的商務物件的新執行個體。 回應要求的商務物件之後，伺服器就會終結的商務物件，並關閉連線。  
  
> [!NOTE]
>  這個行為表示您無法將資料從一個要求傳遞到另一個使用商務物件的屬性或變數。 您必須採用另一種機制，例如檔案或為方法引數，來保存狀態資料。  
  
 類別識別碼 **.RDSDataSpace**物件是 BD96C556-65A3-11 D 0 983A 00C04FC29E36。  
  
 **DataSpace**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [DataSpace 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSpace 物件和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


