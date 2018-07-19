---
title: 查詢屬性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 356121b8980d41a3abf3124d5249164d6d23b4e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247736"
---
# <a name="query-properties-visual-database-tools"></a>查詢屬性 (Visual Database Tools)
  在 [查詢和檢視設計師] 中開啟查詢時，這些屬性會顯示在 [屬性] 視窗中。 除非另有註明，否則您可以在 [屬性] 視窗中編輯這些屬性。  
  
> [!NOTE]  
>  此主題中的屬性是依分類排列，而非依字母順序排列。  
  
## <a name="options"></a>選項。  
 **識別類別目錄**  
 展開以顯示 [名稱] 屬性。  
  
 **名稱**  
 顯示目前查詢的名稱。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中無法予以變更。  
  
 **Database Name**  
 顯示選取資料表的資料來源名稱  
  
 **伺服器名稱**  
 顯示資料來源的伺服器名稱。  
  
 **查詢設計工具分類**  
 展開以顯示其餘屬性。  
  
 **目的資料表**  
 指定要插入資料的資料表名稱。 建立 INSERT 查詢或 MAKE TABLE 查詢時，會出現這份清單。 如果是 INSERT 查詢，請從清單中選取資料表名稱。  
  
 針對 MAKE TABLE 查詢，輸入新資料表的名稱。 若要在其他資料來源中建立目的資料表，請指定完整的資料表名稱，包括目標資料來源名稱、擁有人 (如有需要) 和資料表名稱。  
  
> [!NOTE]  
>  [查詢設計工具] 不檢查名稱是否正在使用中，或您是否具有建立資料表的權限。  
  
 **相異值**  
 指定查詢會篩選結果集中重複的資料。 如果只使用資料表中的一部份資料行，而這些資料行包含了重複的值；或者聯結兩個以上資料表的處理序，會在結果集中產生重複的資料列時，這個選項非常實用。 選擇此選項就等於在 [SQL] 窗格中的陳述式裡插入 DISTINCT 一字。  
  
 **GROUP BY 擴充選項**  
 根據可用的彙總 (Aggregate) 查詢指定查詢的其他選項。 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。  
  
 **輸出全部資料行**  
 指定結果集 (Result Set) 中要包含目前查詢中所有資料表的全部資料行。 選擇此選項就等於在 SQL 陳述式裡的 SELECT 關鍵字後指定星號 (*)，而非指定個別的資料行名稱。  
  
 **查詢參數清單**  
 顯示查詢參數。 若要編輯參數，請按一下屬性，再按屬性右邊的省略符號 ( **…** )。 (只適用於泛型 OLE DB)。  
  
 **SQL 註解**  
 顯示 SQL 陳述式的描述。 若要查看或編輯整個描述，請按一下 [描述]，再按屬性右邊的省略符號 ( **…** )。 您的註解中可能包含使用查詢的人及使用時間等這類資訊 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 (含) 以後版本的資料庫)。  
  
 **排名規格分類**  
 展開以顯示 [Top]、[Percent]、[Expression] 的屬性，以及 [With Ties] 屬性。  
  
 **(Top)**  
 指定查詢將包括 TOP 子句，而這個子句只會傳回結果集內的前 *n* 個資料列，或前百分之 *n* 的資料列。 預設值是查詢會傳回結果集裡前 10 個資料列。  
  
 使用此方塊變更傳回的資料列數目，或指定不同的百分比 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或更新版本)。  
  
 **運算式**  
 指定查詢將傳回的資料列數目或百分比。 如果將 [Percent] 設定為 [是]，則此數字為查詢將傳回的資料列百分比；如果將 [Percent] 設定為 [否]，則此數字表示傳回的資料列數目。 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 (含) 以後版本)。  
  
 **Percent**  
 指定查詢只會傳回結果集內前百分之 *n* 的資料列。 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 (含) 以後版本)。  
  
 **With Ties**  
 指定檢視中會包含 WITH TIES 子句。 如果檢視中包含了 ORDER BY 和以百分比為基礎的 TOP 子句，WITH TIES 非常實用。 如果設定了此選項，而且百分比截止點落在 ORDER BY 子句裡一組相同值的資料列中間，將會擴充檢視以將這些資料列全部包含。 (只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 (含) 以後版本)。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數查詢&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
