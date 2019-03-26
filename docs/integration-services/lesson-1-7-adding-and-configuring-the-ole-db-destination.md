---
title: 步驟 7：新增及設定 OLE DB 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47ba9be2a6ff8a03f40cc6253b0dbd0674e1ec48
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58281822"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>課程 1-7：新增及設定 OLE DB 目的地

您的套件現在可以從一般檔案來源擷取資料，再將該資料轉換成與目的地相容的格式。 下一個工作是要將已轉換的資料載入到目的地。 為了載入資料，您需將 OLE DB 目的地新增到資料流程。 OLE DB 目的地可以使用資料庫資料表、檢視或 SQL 命令，將資料載入到各種 OLE DB 相容的資料庫中。  
  
在此工作中，您會新增及設定 OLE DB 目的地，以使用您先前建立的 OLE DB 連線管理員。  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>新增及設定範例 OLE DB 目的地  
  
1.  在 [SSIS 工具箱] 中展開 [其他目的地]，將 [OLE DB 目的地] 拖曳至 [資料流程] 索引標籤的設計介面中。將 [OLE DB 目的地] 直接放在 [查閱日期索引鍵] 轉換下面。  
  
2.  選取 [查閱日期索引鍵] 轉換，然後將其藍色箭頭拖曳至新的 [OLE DB 目的地]，以連接這兩個元件。  
  
3.  在 [輸入輸出選擇] 對話方塊的 [輸出] 清單方塊中，選取 [查閱比對輸出]，然後選取 [確定]。  
  
4.  在 [資料流程] 設計介面上，於新的 [OLE DB 目的地] 元件中選取 [OLE DB 目的地] 名稱，然後將該名稱變更為**範例 OLE DB 目的地**。  
  
5.  按兩下 [範例 OLE DB 目的地]。  
  
6.  在 [OLE DB 目的地編輯器] 對話方塊中，確定在 [OLE DB 連線管理員] 方塊中已選取 [localhost.AdventureWorksDW2012]。  
  
7.  在 [資料表或檢視表的名稱] 方塊中，輸入或選取 **[dbo].[FactCurrencyRate]**。  
  
8.  選取 [新增] 按鈕以建立新的資料表。  將指令碼中資料表的名稱從 **Sample OLE DB Destination** 變更為 **NewFactCurrencyRate**。  選取 [確定]。  
  
9. 選取 [確定] 時，此對話方塊會關閉，而 [資料表或檢視表的名稱] 則會自動變更為 **NewFactCurrencyRate**。  
  
10. 選取 [對應]。  
  
11. 確認 [AverageRate]、[CurrencyKey]、[EndOfDayRate] 和 [DateKey] 輸入資料行都正確對應到目的地資料行。 如果對應到同名資料行，則表示對應是正確的。  
  
12. 選取 [確定]。  
  
13. 在 [範例 OLE DB 目的地] 目的地上按一下滑鼠右鍵，然後選取 [屬性]。  
  
14. 在 [屬性] 視窗中，確認 [LocaleID] 屬性是設定為 [英文 (美國)]，[DefaultCodePage] 屬性是設為 [1252]。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 8：為第 1 課套件加上註解並設定格式](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>另請參閱  
[OLE DB 目的地](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
