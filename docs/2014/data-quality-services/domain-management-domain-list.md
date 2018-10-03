---
title: 定義域管理：定義域清單 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.domainlist.f1
ms.assetid: 8df305f0-97ea-4226-811b-979ed862e1f0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 20bdaf156d2f2058a05d65385e2c1a63e89dc2eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079088"
---
# <a name="domain-management-domain-list"></a>定義域管理：定義域清單
  此主題描述 **(DQS) 中** [定義域管理] [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 頁面上定義域清單中的控制項。 使用此窗格可選取執行管理作業所在的定義域。 相同的窗格會用於 **[定義域管理]** 頁面上的所有索引標籤式頁面。  
  
## <a name="options"></a>選項。  
  
### <a name="domains-list"></a>定義域清單  
 **網域**  
 此清單會顯示知識庫中的所有定義域。 您在右窗格中的索引標籤式頁面上執行的作業都將針對此清單中選取的定義域執行。 如需相關資訊，請參閱  
  
 **建立複合定義域**  
 在知識庫中建立新的複合定義域。 此命令將會顯示 **[建立複合定義域]** 對話方塊。 若要使用此命令，請以滑鼠右鍵按一下定義域，或是按一下定義域清單上方的圖示。 如需相關資訊，請參閱 [建立複合定義域](../../2014/data-quality-services/create-a-composite-domain.md)。  
  
 **建立定義域**  
 在知識庫中建立新的定義域。 此命令將會顯示 **[建立定義域]** 對話方塊。 若要使用此命令，請以滑鼠右鍵按一下定義域，或是按一下定義域清單上方的圖示。 如需相關資訊，請參閱 [建立定義域](../../2014/data-quality-services/create-a-domain.md)。  
  
 **建立選取之定義域的複本**  
 建立選取之定義域的完全相同複本，並將其加入至知識庫。 其名稱將會是建立它所使用的定義域名稱，且名稱會附加「– 複本」。 若要使用此命令，請以滑鼠右鍵按一下定義域，然後按一下 **[建立複本]**，或是按一下定義域清單上方的圖示。 它無法提供給複合定義域使用。  
  
 **從資料檔匯入定義域**  
 從 .dqs 檔案匯入定義域。 這個命令會顯示 **[從資料檔匯入]** 對話方塊，好讓您瀏覽檔案系統，並針對單一定義域或複合定義域選取 .dqs 檔案。 若要使用此命令，請按一下定義域清單上方的圖示。 如需相關資訊，請參閱 [從 .dqs 檔案匯入定義域](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md)。  
  
 **刪除定義域**  
 從知識庫中刪除選取的定義域。 此命令會顯示 **[SQL Server Data Quality Services]** 對話方塊。 如果您按一下 **[是]**，將永久刪除此定義域及其所有資料。 若要使用此命令，請以滑鼠右鍵按一下定義域，或是按一下定義域清單上方的圖示。  
  
 **建立連結的定義域**  
 建立與選取之定義域連結的定義域。 此命令會顯示 **[建立定義域]** 對話方塊。 若要使用此命令，請以滑鼠右鍵按一下定義域，然後按一下 **[建立連結的定義域]** (連結到選取的定義域)。 您所連結的定義域會顯示在 [建立定義域] 對話方塊中。 此命令無法提供給複合定義域使用。 沒有任何命令可用來取消連結兩個定義域；若要這樣做，請刪除連結的定義域。 無法針對連結的定義域建立連結的定義域。 如需相關資訊，請參閱 [建立連結的定義域](../../2014/data-quality-services/create-a-linked-domain.md)。  
  
 連結的定義域擁有與其連結到的定義域相同的值。 此定義域只有名稱和屬性是不同的。 如果您在連結到的定義域中變更定義域規則、定義域值、參考資料連結或以詞彙為主的關聯，則連結的定義域中的定義域規則、定義域值、參考資料連結或以詞彙為主的關聯也會變更。 此外，如果您在連結的定義域中變更值，也會針對連結到的定義域進行變更。  
  
 **匯出知識庫**  
 將整個知識庫匯出到 .dqs 檔案。 此命令會顯示 **[匯出到資料檔]** 對話方塊。 若要使用此命令，請按一下頁面上方的 **[匯出知識庫資料]** 圖示，或是定義域清單窗格中定義域內容功能表的 **[匯出]** 底下。 如需相關資訊，請參閱 [將知識庫匯出到 .dqs 檔案](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)。  
  
 **匯出定義域**  
 將定義域匯出成 .dqs 檔案。 此命令會顯示 **[匯出到資料檔]** 對話方塊。 若要使用此命令，請按一下頁面上方功能表列中的 **[匯出]** 功能表，或是以滑鼠右鍵按一下定義域清單窗格。 如需相關資訊，請參閱 [將定義域匯出成 .dqs 檔案](../../2014/data-quality-services/export-a-domain-to-a-dqs-file.md)。  
  
  
