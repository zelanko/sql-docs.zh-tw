---
title: 基本 RDS 程式設計模型 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65dea5ebf2813267ef7e7bb83f2f37209ee2114f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720876"
---
# <a name="basic-rds-programming-model"></a>基本 RDS 程式設計模型
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 位址存在下列環境中的應用程式： 用戶端應用程式指定將在伺服器與要傳回的所需的資訊所需的參數執行的程式。 在指定的資料來源，以提升存取伺服器上叫用的程式擷取的資訊、 選擇性地處理資料，和將產生的資訊傳回用戶端應用程式的表單，它可以輕鬆地使用。 RDS 可讓您執行下列動作順序的方法：  
  
-   指定要在伺服器上，叫用的程式，並取得用來從用戶端參考它。 (有時稱為 「 此參照*proxy*。 它代表遠端伺服器的程式。 用戶端應用程式會 「 呼叫 」 proxy 視為就像是本機的程式，但它實際上會叫用的遠端伺服器的程式。）  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式識別資料來源以及要發出的命令。 （伺服器程式實際上會使用 ADO 來存取資料來源。 ADO 使用其中一個指定的參數，進行連線並發行另一個參數中指定的命令。）  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料來源的物件。 （選擇性）**資料錄集**物件在伺服器上處理。  
  
-   伺服器程式會傳回最後**資料錄集**用戶端應用程式的物件。  
  
-   在用戶端**資料錄集**物件放入容易使用的視覺控制項的表單。  
  
-   修改**資料錄集**物件傳送至伺服器的程式，可使用它們來更新資料來源。  
  
 這個程式設計模型包含特定的便利功能。 如果您不需要複雜的伺服器程式存取資料來源，如果您提供必要的連接和命令參數，RDS 會自動擷取指定的資料，使用簡單的預設伺服器計劃。  
  
 如果您需要更複雜的處理，您可以指定自己的自訂伺服器程式。 比方說，自訂伺服器計劃有 ADO 的完整功能，其可供使用，因為它無法連接到數個不同的資料來源、 一些複雜的方式，結合他們的資料，然後傳回用戶端應用程式的 簡單、 已處理的結果。  
  
 最後，如果您的需求將會是某處之間，ADO 現在支援自訂的預設伺服器程式的行為。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 程式設計模型詳述](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


