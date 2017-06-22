---
title: "設計資料庫圖表 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 39d9220dc13546a5a1e9c95d034b5a5cf0ac43b5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="design-database-diagrams-visual-database-tools"></a>設計資料庫圖表 (Visual Database Tools)
「資料庫設計工具」為視覺化工具，可讓您設計連接的資料庫，並將該資料庫視覺化。 設計資料庫時，您可以使用資料庫設計工具建立、編輯或刪除資料表、資料行、索引鍵、索引、關聯性和條件約束。 若要以視覺化方式呈現資料庫，可以建立一或多個圖表說明該資料庫中部分或全部的資料表、資料行、索引鍵和關聯性。  
  
![說明資料表關聯性的資料庫圖表](../../ssms/visual-db-tools/media/dv3w7c1.gif "說明資料表關聯性的資料庫圖表")  
  
您可以根據您的需要在任何資料庫中建立資料庫圖表 (不限個數)；不論圖表數量為何，每個圖表中都將出現資料庫表格。 因此您可建立不同的圖表，將資料庫的不同部份進行視覺化，或強調不同的設計重點。 例如，您可以建立大型圖表來顯示所有資料表和資料行，以及建立小型圖表來顯示所有的資料表，但不顯示資料行。  
  
您建立的所有資料庫圖表都將存放在相關資料庫中。  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>資料庫圖表中的資料表和資料行  
資料庫圖表中的每個資料表都具有三項功能：標題列、資料列選取器和一組屬性欄位。  
  
**標題列** ：標題列顯示資料表的名稱  
  
如果您已經修改某個資料表但尚未儲存，該資料表名稱的後方將出現星號 (*) 表示尚未儲存變更。 如需儲存修改過的資料表和圖表的詳細資訊，請參閱 [Work with Database Diagrams &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
**資料列選取器** ：您可以按一下資料列選取器，選取資料表中的資料庫資料行。 如果該資料行位於資料表的主索引鍵，資料列選取器將顯示索引鍵符號。 如需主索引鍵的詳細資訊，請參閱 [使用索引鍵 (Visual Database Tools)](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd)。  
  
**屬性資料行** ：屬性資料行組只有在資料表中的特定檢視才可見。 您可以使用五種檢視方法來檢視資料表，任何一種方法都可以協助您管理圖表的大小和配置。  
  
如需資料表檢視的詳細資訊，請參閱[自訂圖表中顯示的資料量 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)。  
  
## <a name="relationships-in-a-database-diagram"></a>資料庫圖表中的關聯性  
資料庫圖表中的每個關聯性都具有三項功能：結束點、行樣式和相關資料表。  
  
**結束點** ：行的結束點可以顯示其關聯性為一對一或一對多。 如果關聯性在結束點具有一個索引鍵，且在其他結束點擁有 ∞，該關聯性即為一對多關聯性 (One-To-Many Relationship)。 如果關聯性在每個結束點都擁有一個索引鍵，該關聯性即為一對一關聯性。  
  
**行樣式** ：資料行本身 (非其結束點) 可指出當新資料加入至外部索引鍵表格時，資料庫管理系統 (DBMS) 是否會強制使用關聯性的參考完整性 (Referential Integrity)。 如果該行為實線，當您在外部索引鍵資料表中加入或修改資料列時，DBMS 將強制使用關聯性的參考完整性。 如果該行為虛線，當您在外部索引資料表中加入或修改資料列時，DBMS 將不會強制使用關聯性的參考完整性。  
  
**相關資料表** ：關聯性行將指出兩個表格之間是否存在外部索引鍵關聯性。 如果是一對多關聯性，外部索引鍵表即為該行 ∞ 符號旁的資料表。 如果該行的兩個結束點都與同一個資料表連接，則該關聯性即為自反關聯性 (Reflexive Relationship)。 如需詳細資訊，請參閱[繪製自反關聯性 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/draw-reflexive-relationships-visual-database-tools.md)。  
  
## <a name="in-this-section"></a>本章節內容  
[了解資料庫圖表擁有權 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
  
[在資料庫圖表設計工具中導覽 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/navigate-in-database-diagram-designer-visual-database-tools.md)  
  
[設定資料庫圖表設計工具 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  
[升級舊版的資料庫圖表 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
[開啟資料庫圖表設計工具 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>另請參閱  
[使用資料庫圖表 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[使用資料庫圖表中的資料表 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
[使用圖表配置 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  

