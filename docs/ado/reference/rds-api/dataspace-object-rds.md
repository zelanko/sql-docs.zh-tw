---
title: DataSpace 物件 (RDS) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 078799f90a0241dc29f30693adce95ea2e795ff8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654266"
---
# <a name="dataspace-object-rds"></a>DataSpace 物件 (RDS)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 建立自訂商務物件位於中介層上的用戶端 proxy。  
  
 遠端資料服務需要商務物件 proxy，以便用戶端元件可以與位於中介層商務物件通訊。 封裝、 unpackaging，和傳輸 （封送處理） 的應用程式，幫助 proxy[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)跨處理序或電腦界限的資料。  
  
 遠端資料服務會使用**rds。DataSpace**物件的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法用來建立商務物件 proxy。 每當建立它的中介層商務物件互相對應的執行個體時，動態建立商務物件 proxy。 遠端資料服務支援下列通訊協定： HTTP、 HTTPS （HTTP 安全通訊端）、 DCOM 和同處理序 （用戶端元件和商務物件位於相同的電腦上）。  
  
> [!NOTE]
>  以 「 無狀態 」 的方式運作的 RDS 時**rds。DataSpace**物件使用的 HTTP 或 HTTPS 通訊協定。 也就是伺服器傳回回應之後，會捨棄任何有關用戶端要求的內部資訊。  
  
> [!NOTE]
>  雖然商務物件出現有的商務物件 proxy 存留期，商務物件確實存在才將回應傳送的要求。 當發出要求 （也就是一種方法會叫用的商務物件），proxy 便會開啟新的連接到伺服器，並在伺服器建立商務物件的新執行個體。 回應要求的商務物件之後，伺服器就會終結的商務物件，並關閉連線。  
  
> [!NOTE]
>  這個行為表示您無法將資料從一個要求傳遞到另一個使用商務物件屬性或變數。 您必須採用另一種機制，例如檔案或方法的引數，來保存狀態資料。  
  
 頇蜞頇**rds。DataSpace**物件是 BD96C556-65A3-11 D 0 983A 00C04FC29E36。  
  
 **DataSpace**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [DataSpace 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSpace 物件和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


