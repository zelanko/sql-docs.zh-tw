---
description: 什麼是資料指標？
title: 什麼是資料指標？ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: rothja
ms.author: jroth
ms.openlocfilehash: 3090e38507a73d00edbe3bd1cb85e408c88fdba1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978919"
---
# <a name="what-is-a-cursor"></a>什麼是資料指標？
關聯式資料庫中的作業會針對完整的資料列集運作。 由 SELECT 陳述式所傳回的資料列集包括所有滿足陳述式 WHERE 子句之條件的資料列。 由陳述式傳回的完整資料列稱為結果集。 應用程式（尤其是互動式和線上的應用程式）不一定能以一個單位有效地使用整個結果集。 這些應用程式需要一個機制，一次運用一個資料列或小型資料列區塊。 資料指標就是一種結果集的擴充，提供此種機制。  
  
 資料指標是由資料指標程式庫所執行。 資料指標程式庫是一種軟體，通常會實作為資料庫系統或資料存取 API 的一部分，用來管理從資料來源傳回的資料屬性， (結果集) 。 這些屬性包括並行管理、結果集內的位置、傳回的資料列數目，以及您是否可以透過結果集 (捲動) ，向前或向後移動 (或) 。  
  
 資料指標會持續追蹤結果集中的位置，並可讓您針對結果集執行多個作業（逐列），不論是否傳回原始資料表。 換句話說，資料指標會根據資料庫中的資料表，以概念方式傳回結果集。 資料指標的命名方式是因為它會指出結果集內目前的位置，就像電腦螢幕上的游標指出目前的位置一樣。  
  
 請務必先熟悉資料指標的概念，然後再繼續瞭解它們在 ADO 中的用法細節。  
  
 使用資料指標，您可以：  
  
-   指定結果集中特定資料列的定位。  
  
-   根據目前的結果集位置，抓取一個資料列或資料列區塊。  
  
-   修改結果集中目前位置的資料列中的資料。  
  
-   針對其他使用者所做的資料變更，定義不同的敏感度層級。  
  
 例如，假設有一個應用程式會顯示潛在買方的可用產品清單。 買方會在清單中滾動以查看產品詳細資料和成本，最後選取要購買的產品。 清單的其餘部分會進行額外的滾動和選取。 在買方的考慮下，產品會一次顯示一個，但應用程式會使用可滾動的資料指標來向上和向下流覽結果集。  
  
 您可以使用各種不同的方式來使用資料指標：  
  
-   完全不使用任何資料列。  
  
-   使用單一資料表中的部分或所有資料列。  
  
-   包含邏輯聯結資料表中的部分或所有資料列。  
  
-   唯讀或可在資料指標或欄位層級進行更新。  
  
-   順向或完全可滾動。  
  
-   使用位於伺服器上的資料指標索引鍵集。  
  
-   區分其他應用 (程式所造成的基礎資料表變更，例如成員資格、排序、插入、更新和刪除) 。  
  
-   存在於伺服器或用戶端上。  
  
 唯讀資料指標可協助使用者流覽結果集，而讀取/寫入資料指標可執行個別的資料列更新。 您可以使用指向資料表資料列的索引鍵集來定義複雜資料指標。 雖然有些資料指標是以正向方向的唯讀資料指標，但其他資料指標可以來回移動，並且根據其他應用程式對資料庫所做的變更，提供結果集的動態重新整理。  
  
 並非所有應用程式都必須使用資料指標來存取或更新資料。 有些查詢不需要使用資料指標進行直接資料列更新。 資料指標應該是您選擇用來取出資料的最後一項技術，然後您應該選擇可能的最低影響資料指標。 當您使用預存程式建立結果集時，無法使用資料指標編輯或 update 方法來更新結果集。  
  
## <a name="concurrency"></a>並行  
 在某些多使用者的應用程式中，向使用者呈現的資料非常重要。 這類系統的典型範例是航空公司預訂系統，其中許多使用者可能會在特定航班上爭用相同的基座 (因此，) 的單一記錄。 在這樣的情況下，應用程式設計必須處理單一記錄上的並行作業。  
  
 在其他應用程式中，並行處理並不重要。 在這種情況下，將資料保持在最新的隨時都不會有費用。  
  
## <a name="position"></a>位置  
 資料指標也會持續追蹤結果集內的目前位置。 將游標位置視為目前記錄的指標，類似于陣列索引指向陣列中該特定位置之值的方式。  
  
## <a name="scrollability"></a>可捲動性  
 您的應用程式所使用的資料指標類型，也會影響在結果集的資料列中向前及向後移動的能力;這有時稱為捲動。 向前 *和* 向後移動結果集的能力會增加資料指標的複雜度，因此需要更高的成本來執行。 基於這個理由，您應該只在必要時才使用此功能要求資料指標。
