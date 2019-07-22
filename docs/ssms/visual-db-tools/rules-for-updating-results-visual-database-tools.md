---
title: 更新結果的規則 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bef3b9612b68c253fed032fe63d5d67e61816dff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255670"
---
# <a name="rules-for-updating-results-visual-database-tools"></a>更新結果的規格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
大多數的情形下，您可以更新 [結果窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)所顯示的結果集。 不過也有些情形無法更新。  
  
一般說來，為了更新結果， [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 必須要有足夠的資訊才能唯一識別資料表中的資料列。 一個例子是輸出清單中的查詢包含主索引鍵。 此外，也必須要有足夠的使用權限可更新資料庫。  
  
如果查詢以檢視做為依據，可能可以更新。 同樣的原則不只套用至檢視本身，但檢視中套用至基礎資料表除外。  
  
> [!NOTE]  
> [查詢和檢視設計師] 無法事先判斷以檢視做為依據的結果集是否能更新。 因此即使不能更新，也會顯示出所有的檢視。  
  
下表是具體例項的摘要，說明 [結果] 窗格中的查詢結果有的可以、有的不能更新。 在許多情況下，使用的資料庫會指定查詢結果是否能更新。  
  
|查詢|結果能否更新？|  
|---------|---------------------------|  
|查詢是根據輸出清單中有主索引鍵的一份資料表|能 (不含下列清單)。|  
|查詢是根據不含唯一索引，也沒有主索引鍵的一份資料表|依照查詢和資料庫而定。 如果有足夠的資訊則可單獨識別出記錄，有些資料庫允許更新。|  
|查詢是根據未相連結的多份資料表|資料分割|  
|查詢是根據資料庫中標記為唯讀的資料|資料分割|  
|查詢是根據一份檢視，牽涉無條件約束 (Constraint) 的一份資料表|能 (不含下列清單)。|  
|查詢是根據一對一關聯性 (One-To-One Relationship) 所連結的資料表|能 (不含下列清單)。|  
|查詢是根據一對多關聯性 (One-To-Many Relationship) 所連結的資料表|通常可以。|  
|查詢是根據三份以上的資料表，具有多對多關聯性 (Many-To-Many Relationship)|資料分割|  
|查詢是根據未獲得更新使用權限的一份資料表|可刪除但不能更新。|  
|查詢是根據未獲得刪除使用權限的一份資料表|可更新但不能刪除。|  
|彙總查詢 (Aggregate Query)|資料分割|  
|查詢是根據包含總計或彙總函式 (Aggregate Function) 的子查詢 (Subquery)|資料分割|  
|查詢包含有 DISTINCT 關鍵字，以排除重複的資料列|資料分割|  
|查詢的 FROM 子句包含使用者自訂的函數，可傳回資料表，而且此使用者自訂的函數並包含多選陳述式|資料分割|  
|查詢的 FROM 子句包含使用者自訂的內嵌 (Inline) 函數|是的。|  
  
此外，查詢結果中可能有特定的資料行無法更新。 以下的清單是資料行特定類型的摘要，[結果] 窗格不能更新。  
  
-   資料行是根據運算式  
  
-   資料行是根據純量的使用者自訂函數  
  
-   資料列或資料行由其他使用者刪除  
  
-   資料列或資料行由其他使用者鎖定 (鎖定的資料列通常解除鎖定即可更新)  
  
-   時間戳記或 BLOB 資料行  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
