---
description: DataSpace 物件 (RDS)
title: " (RDS) 的空間物件 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 092af21c57b733e12c233cb201304cbc27930c80
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768377"
---
# <a name="dataspace-object-rds"></a>DataSpace 物件 (RDS)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 建立位於仲介層的自訂商務物件之用戶端 proxy。  
  
 遠端資料服務需要商務物件 proxy，才能讓用戶端元件與位於仲介層的商務物件進行通訊。 Proxy 有助於封裝、解除封裝和傳輸 (封送處理跨進程或電腦界限的應用程式 [記錄集](../ado-api/recordset-object-ado.md) 資料) 。  
  
 遠端資料服務會使用 **RDS。** 用來建立商務物件 proxy 的空間物件 [CreateObject](./createobject-method-rds.md) 方法。 只要建立其中介層商務物件對應項的實例，就會以動態方式建立商務物件 proxy。 遠端資料服務支援下列通訊協定： HTTP、HTTPS (HTTP 安全通訊端) 、DCOM 以及同進程 (用戶端元件，以及商務物件位於) 的相同電腦上。  
  
> [!NOTE]
>  Rds 在 Rds 時以「無狀態」的方式運作 **。空間** 物件會使用 HTTP 或 HTTPS 通訊協定。 也就是說，在伺服器傳迴響應之後，會捨棄用戶端要求的任何內部資訊。  
  
> [!NOTE]
>  雖然商務物件的存留期似乎存在於商務物件 proxy 的存留期內，但只有在將回應傳送給要求時，商務物件才會存在。 發出要求時 (也就是在商務物件) 上叫用方法，proxy 會開啟新的伺服器連接，而伺服器會建立商務物件的新實例。 在商務物件回應要求之後，伺服器會終結商務物件並關閉連接。  
  
> [!NOTE]
>  此行為表示您不能使用商務物件屬性或變數，將資料從某個要求傳遞到另一個要求。 您必須使用一些其他機制（例如檔案或方法引數）來保存狀態資料。  
  
 RDS 的類別識別碼 **。** 已 BD96C556-65A3-11D0-983A-00C04FC29E36 空間物件。  
  
 您可以安全地執行腳本處理的 **空間** 物件。  
  
 本節包含下列主題。  
  
-   [DataSpace 物件 (RDS) 屬性、方法和事件](./dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSpace 物件和 CreateObject 方法範例 (VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)