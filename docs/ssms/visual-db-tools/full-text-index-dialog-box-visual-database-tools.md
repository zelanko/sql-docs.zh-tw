---
title: "全文檢索索引對話方塊 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c81ecbf34a24d718f891987e396a2a4e7beabfa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>全文檢索索引對話方塊 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 這個對話方塊可讓您建立全文檢索索引，以便在資料庫資料表的文字資料行上進行全文檢索搜尋。 全文檢索索引必須藉助一般索引，因此您必須先建立一般索引。 您必須在單一、非 Null 的資料行上建立一般索引，而且最好選擇值較小的資料行，而不要選擇包含大數值的資料行。  
  
> [!NOTE]  
> 若要建立全文檢索索引，您必須先對使用外部工具的資料庫建立全文檢索，例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 Enterprise Manager。  
  
> [!NOTE]  
> 並非每個 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]版本都可使用全文檢索索引功能。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)。  
  
## <a name="options"></a>選項。  
**選取的全文檢索索引**  
列出現有的全文檢索索引。 選取索引，在方格右側顯示其屬性。 如果清單是空的，表示資料表尚未定義全文檢索關聯性。  
  
**[加入]**  
建立新的全文檢索索引。  
  
**刪除**  
刪除在 [選取的全文檢索索引] 清單中所選取的全文檢索索引。  
  
**一般類別目錄**  
展開時會顯示 [資料行] 和 [全文檢索資料庫目錄名稱]。  
  
**資料行**  
顯示可使用全文檢索搜尋資料行的逗號分隔清單。 若要查看完整清單，請按屬性欄位左側的省略符號按鈕 (**…**)。  
  
**全文檢索資料庫目錄名稱**  
顯示全文檢索索引儲存位置的全文檢索資料庫目錄名稱。 若要將索引儲存到不同的目錄，請按目錄名稱，然後從下拉式清單選擇另外一個目錄名稱。  
  
> [!NOTE]  
> 目錄必須先在外部工具建立，例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 Enterprise Manager。  
  
**識別類別目錄**  
展開時會顯示這個索引的名稱欄位。  
  
**名稱**  
顯示這個全文檢索索引的系統指定名稱。  
  
**資料表設計工具類別目錄**  
展開時會顯示指示索引如何執行的屬性。  
  
**作用中**  
指示是否能夠使用這個全文檢索索引執行全文檢索搜尋。  
  
**變更追蹤設定**  
描述這個索引的變更追蹤狀態：[手動]、[自動] 或 [關閉]。  
  
**搜耙已完成**  
顯示最近的搜耙是否已經完成。 如果這個屬性的值為 [否]，表示搜耙目前正在進行。  
  
**目前或上一個搜耙的結束日期及時間**  
顯示最近搜耙結束的日期和時間。  
  
**目前或上一個搜耙中的錯誤**  
顯示目前或最近之搜耙的錯誤數目。  
  
**索引版本**  
顯示搜耙開始時的資料表結構描述版本。  
  
**目前或上一個搜耙中的資料列**  
顯示目前或最近搜耙中更新之資料列的數目。  
  
**目前或上一個搜耙的開始日期及時間**  
顯示目前或最近搜耙開始的日期和時間。  
  
**下一個搜耙的時間戳記**  
顯示下一個搜耙將會開始的日期和時間。  
  
**目前或上一個搜耙的類型**  
顯示目前或最近搜耙的類型：[完整]、[累加]、[更新] 或 [自動傳用]。  
  
**唯一索引名稱**  
顯示這個資料庫中擁有唯一單一資料行索引的所有資料行名稱的清單。 這些資料行可用來建立全文檢索索引。  
  
## <a name="see-also"></a>另請參閱  
[使用全文檢索索引精靈](http://msdn.microsoft.com/en-us/3e9d9605-6525-4781-9168-fdaa06db3459)  
[CREATE FULLTEXT INDEX (Transact-SQL)](http://msdn.microsoft.com/en-us/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)  
  
