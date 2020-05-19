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
author: rothja
ms.author: jroth
ms.openlocfilehash: 441d3f9f2de12e269839c3561dd0d202121018be
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750182"
---
# <a name="basic-rds-programming-model"></a>基本 RDS 程式設計模型
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 會解決存在於下列環境中的應用程式：用戶端應用程式會指定將在伺服器上執行的程式，以及傳回所需資訊所需的參數。 在伺服器上叫用的程式會取得指定資料來源的存取權、抓取資訊，並選擇性地處理資料，然後將產生的資訊以容易使用的形式傳回至用戶端應用程式。 RDS 提供執行下列動作順序的方法：  
  
-   指定要在伺服器上叫用的程式，並取得從用戶端參考它的方式。 （此參考有時稱為*proxy*。 它代表遠端伺服器程式。 用戶端應用程式會「呼叫」 proxy，如同它是本機程式一樣，但實際上會叫用遠端伺服器程式）。  
  
-   叫用伺服器程式。 將參數傳遞給識別資料來源的伺服器程式，以及要發出的命令。 （伺服器程式實際上會使用 ADO 來取得資料來源的存取權。 ADO 會使用其中一個指定的參數進行連接，然後發出另一個參數中指定的命令。）  
  
-   伺服器程式會從資料來源取得[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 （選擇性）在伺服器上處理**記錄集**物件。  
  
-   伺服器程式會將最終的**記錄集**物件傳回至用戶端應用程式。  
  
-   在用戶端上，**記錄集**物件會放入可供視覺控制項輕鬆使用的表單中。  
  
-   對**記錄集**物件所做的任何修改都會傳送回伺服器程式，這會使用它們來更新資料來源。  
  
 此程式設計模型包含某些便利功能。 如果您不需要複雜的伺服器程式來存取資料來源，而且您提供必要的連接和命令參數，則 RDS 會自動以簡單的預設伺服器程式來取得指定的資料。  
  
 如果您需要更複雜的處理，您可以指定自己的自訂伺服器程式。 例如，由於自訂伺服器程式具有 ADO 的全部強大功能，因此它可以連接到數個不同的資料來源，以某種複雜的方式結合其資料，然後將一個簡單的已處理結果傳回給用戶端應用程式。  
  
 最後，如果您的需求介於其間的某個位置，ADO 現在支援自訂預設伺服器程式的行為。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 程式設計模型詳細資料](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


