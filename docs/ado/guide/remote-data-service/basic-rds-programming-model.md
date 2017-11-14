---
title: "基本 RDS 程式設計模型 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d99d092b91ed150a3ad9163f2c4f7e513554e9f4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="basic-rds-programming-model"></a>基本 RDS 程式設計模型
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 位址存在下列環境中的應用程式： 用戶端應用程式指定的伺服器，並傳回所需的資訊所需的參數，也會執行程式。 叫用指定的資料來源，以提升存取伺服器上的程式擷取的資訊、 選擇性地處理資料，並再將產生的資訊傳回給用戶端應用程式的形式，它可以輕鬆地使用。 RDS 提供的方式，讓您為執行下列動作順序：  
  
-   指定要在伺服器上，叫用程式，並取得從用戶端指的方式。 (有時稱為這個參考*proxy*。 它代表遠端伺服器上的程式。 用戶端應用程式會 「 呼叫 」 proxy 視為就像是本機程式，但它實際上會叫用的遠端伺服器的程式。）  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式的識別資料來源以及要發出的命令。 （伺服器程式實際上會使用 ADO 來存取資料來源。 ADO 連接與其中一個指定的參數，並接著發出另一個參數中指定的命令。）  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料來源的物件。 （選擇性）**資料錄集**物件在伺服器上處理。  
  
-   伺服器程式傳回最終**資料錄集**用戶端應用程式的物件。  
  
-   在用戶端，**資料錄集**物件放入一個表單，可能容易使用的視覺控制項。  
  
-   任何修改**資料錄集**物件傳送至伺服器的程式，可使用它們來更新資料來源。  
  
 這個程式設計模型包含特定方便的功能。 如果您不需要複雜的伺服器程式存取資料來源，而且如果您提供必要的連接和命令參數，RDS 會自動擷取與簡單的預設伺服器程式指定的資料。  
  
 如果您需要更複雜的處理，您可以指定您自己自訂的伺服器的程式。 比方說，自訂伺服器程式已在進行處置時 ADO 的完整功能，因為它無法連接到數個不同的資料來源、 複雜的方式，以合併它們的資料，然後傳回用戶端應用程式的 簡單、 已處理的結果。  
  
 最後，如果您需要的地方之間，ADO 現在支援自訂的預設伺服器程式的行為。  
  
## <a name="see-also"></a>另請參閱  
 [在詳細資料的 RDS 程式設計模型](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



