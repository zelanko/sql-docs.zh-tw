---
title: 步驟 7：加入和設定 OLE DB 目的地 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 97b155852a0d6941cff4da0bdd4565e08dc63e79
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393086"
---
# <a name="step-7-adding-and-configuring-the-ole-db-destination"></a>步驟 7：加入和設定 OLE DB 目的地
  現在，封裝可以從一般檔案來源中擷取資料，再將資料轉換成與目的地相容的格式。 下一項工作是要把已轉換的資料實際載入到目的地。 若要載入資料，您必須將 OLE DB 目的地加入資料流程中。 OLE DB 目的地可使用資料庫資料表、檢視或 SQL 命令，將資料載入到各種 OLE DB 相容資料庫中。  
  
 在這個程序中，您加入和設定 OLE DB 目的地來使用您先前建立的 OLE DB 連接管理員。  
  
### <a name="to-add-and-configure-the-sample-ole-db-destination"></a>若要加入和設定範例 OLE DB 目的地  
  
1.  在 [SSIS 工具箱] 中展開 [其他目的地]，將 [OLE DB 目的地] 拖曳至 [資料流程] 索引標籤的設計介面中。將 OLE DB 目的地直接放在 [查閱日期索引鍵] 轉換下面。  
  
2.  按一下 [查閱日期索引鍵] 轉換，將綠色箭頭拖曳至新加入的 [OLE DB 目的地]，來連接這兩個元件。  
  
3.  在 [輸入輸出選擇] 對話方塊的 [輸出] 清單方塊中，按一下 [查閱比對輸出]，然後按一下 [確定]。  
  
4.  在 [資料流程] 設計介面上，於新加入的 [OLE DB 目的地] 元件中按一下 [OLE DB 目的地]，將名稱變更為**範例 OLE DB 目的地**。  
  
5.  按兩下 [範例 OLE DB 目的地]。  
  
6.  在 [OLE DB 目的地編輯器] 對話方塊中，確定已在 [OLE DB 連線管理員] 方塊中選取 [localhost.AdventureWorksDW2012]。  
  
7.  在 [資料表或檢視的名稱] 方塊中，輸入或選取 **[dbo].[FactCurrencyRate]**。  
  
8.  按一下 [新增] 按鈕，建立新的資料表。  在指令碼中變更資料表的名稱，使其成為 **NewFactCurrencyRate**。  按一下 [確定] 。  
  
9. 按一下 [確定] 後，此對話方塊將會關閉，而且 [資料表或檢視表的名稱] 將會自動變更為 [NewFactCurrencyRate]。  
  
10. 按一下 [對應]。  
  
11. 確認 [AverageRate]、[CurrencyKey]、[EndOfDayRate] 和 [DateKey] 輸入資料行都正確對應到目的地資料行。 如果對應到同名資料行，則表示對應是正確的。  
  
12. 按一下 [確定] 。  
  
13. 以滑鼠右鍵按一下 [範例 OLE DB 目的地] 目的地，然後按一下 [屬性]。  
  
14. 在 [屬性] 視窗中，確認`LocaleID`屬性設定為**英文 （美國）** 並`DefaultCodePage`屬性設定為**1252年**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 8：使第 1 課封裝更容易了解](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 目的地](data-flow/ole-db-destination.md)  
  
  
