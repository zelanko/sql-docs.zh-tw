---
title: 資料成形概觀 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d693ccbeb06860cd4633a933e80b9ccbe6526a8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702231"
---
# <a name="data-shaping-overview"></a>資料成形概觀
*資料成形*表示建置在查詢中的兩個或多個邏輯項目之間的階層式關聯性。 階層中所見的其中一個記錄之間的父子式關聯性[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)，和一或多個記錄 （也稱為一章） 的另一個**資料錄集**。 在父子式關聯性，父代**Recordset**包含子系**資料錄集**。 客戶和訂單這類的階層式關聯性的範例。 在資料庫中每位客戶，可以有零個或多個訂單。 階層式關聯性可以是遞迴的這表示可以在子記錄中巢狀孫系的記錄。 基本上，可以任意深度巢狀階層式資料錄。 在實務上，ADO 會限制為最多 512 個遞迴**資料錄集**s。  
  
 在一般情況下，資料行的形狀**資料錄集**可包含從資料提供者，例如 Microsoft® SQL Server，另一個的參考資料**資料錄集**，值衍生自的單一資料列的計算**資料錄集**，或從作業衍生的整個資料行的值**資料錄集**。 資料行也可以新製作和空白。  
  
 當您擷取包含另一個的參考資料行的值**Recordset**，ADO 會自動將傳回的實際**資料錄集**參考所表示。 參考**Recordset**是實際的子系，稱為子集合的參考*章*。 在單一父系可以參考多個子**資料錄集**。  
  
 資料成形的 ADO 支援可讓您查詢資料來源，並傳回**Recordset**所在的 （父系） 筆記錄均代表 （子系）**資料錄集**。 在客戶-訂單案例中，您可以使用資料成形以擷取客戶的資訊，以及在單一查詢中每個客戶所下訂單。 結果**Recordset**也稱為形狀**資料錄集**。  
  
 此外，在 ADO 中塑造資料可讓您建立新**Recordset**物件，而不使用基礎資料來源**新增**關鍵字，描述欄位的父和子**資料錄集**。 新**資料錄集**物件然後要填入資料，並持續儲存。 開發人員也可以執行各種計算或彙總 (例如**總和**， **AVG**，並**最大**) 子欄位。 資料成形也可以建立父代**資料錄集**從子系**資料錄集**群組子系中的記錄，並將一個資料列放入子系中每個群組的父代。  
  
 一般 SQL 可讓您擷取使用資料**聯結**語法，但這可能會沒有效率且不易處理因為備援的父資料會在每一筆記錄，傳回指定的父子式關聯性重複。 資料成形可以產生關聯的父項中的單一父記錄**Recordset**子系中的多個子記錄**資料錄集**，避免的備援性**聯結**。 多數人覺得父子式多重**資料錄集**程式設計模型更自然也更輕鬆地使用比單一**加入資料錄集**模型。
