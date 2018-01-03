---
title: "資料成形概觀 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9720e3312332fe0c4a00bac01cbaa82908125dfb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="data-shaping-overview"></a>資料成形概觀
*資料成形*表示要建立兩個或多個查詢中的邏輯實體之間的階層式關聯性。 中的其中一個記錄之間的父子式關聯性，可以看到階層[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，和一或多個記錄 （也稱為章） 的另一個**資料錄集**。 在父子式關聯性，父系**資料錄集**含有子系**資料錄集**。 舉例來說，這類的階層式關聯性是客戶和訂單。 在資料庫中每位客戶，可以有零個或多個訂單。 階層式關聯性可以是遞迴的這表示孫系記錄可以巢狀子記錄中。 原則上，可以任意深度巢狀階層式記錄。 在實務上，ADO 會限制為最多 512 個遞迴**資料錄集**s。  
  
 在一般情況下，資料行的形狀**資料錄集**可包含從資料提供者，例如 Microsoft® SQL Server，另一個的參考資料**資料錄集**，衍生自的單一資料列計算的值**資料錄集**，或從作業衍生的整個資料行的值**資料錄集**。 資料行也可以新優質和空白。  
  
 當您擷取包含另一個的參考資料行的值**資料錄集**，ADO 會自動將傳回的實際**資料錄集**參考所表示。 若要參考**資料錄集**是實際的子系，稱為子集合的參考*章*。 在單一父系可以參考一個以上的子系**資料錄集**。  
  
 ADO 支援資料成形可讓您查詢資料來源，並傳回**資料錄集**（父系） 記錄代表 （子系）**資料錄集**。 在客戶-訂單案例中，您可以使用資料成形，擷取客戶的資訊，以及在單一查詢中的每個客戶所下的訂單。 產生**資料錄集**也稱為形狀**資料錄集**。  
  
 此外，在 ADO 中塑造資料可讓您建立新**資料錄集**沒有基礎資料來源使用的物件**新增**關鍵字來描述的父和子欄位**資料錄集**。 新**資料錄集**物件可以則填入資料，而且持續儲存。 開發人員也可以執行各種計算或彙總 (例如，**總和**， **AVG**，和**最大**) 的子欄位。 資料成形也可以建立父**資料錄集**從子系**資料錄集**群組之子系的記錄，並將一個資料列放置在每個群組之子系的父系。  
  
 一般 SQL 可讓您擷取使用資料**聯結**語法，但是這樣可能沒有效率且變得不便因為多餘的父資料會傳回指定的父子式關聯性的每一筆記錄中重複。 資料成形可以相關聯的父系中的單一父記錄**資料錄集**之子系的多個子記錄**資料錄集**，避免的備援性**聯結**。 多數人覺得父子式多重**資料錄集**程式設計模型更自然且輕鬆地使用比單一**加入資料錄集**模型。
