---
title: 建立、修改及刪除發行集和發行項 (複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
ms.assetid: e66d06ec-a12b-444d-875b-77f958af2f21
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f5d375a46a4e158311e5005dc8bf7c3b2627bc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-modify-and-delete-publications-and-articles-replication"></a>建立、修改及刪除發行集和發行項 (複寫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  文件集的這一章節包含建立發行集和定義發行項之相關工作的程序資訊。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [刪除發行集](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [刪除發行項](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [從 Oracle 資料庫建立發行集](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [設定訂閱的到期時間](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [複寫結構描述變更](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [管理識別資料行](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [設定合併式發行集的相容性層級](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
## <a name="snapshot-options"></a>快照集選項  
  
-   [指定快照集格式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-snapshot-format-sql-server-management-studio.md)  
  
-   [指定替代快照集資料夾位置 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [壓縮快照集檔案 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [在套用快照集的前後執行指令碼 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [透過 FTP 傳遞快照集](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
## <a name="filtering-data"></a>篩選資料  
  
-   [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [最佳化參數化資料列篩選](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [定義和修改合併發行項之間的聯結篩選](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
-   [在合併發行項之間自動產生一組聯結篩選 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)  
  
## <a name="transactional-replication-options"></a>異動複寫選項  
  
-   [設定對交易式發行項之資料變更的傳播方法](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [啟用交易式發行集的更新訂閱](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
-   [設定佇列的更新衝突解決選項 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   [在交易式發行集中發行預存程序的執行項 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
## <a name="merge-replication-options"></a>合併式複寫選項  
  
-   [定義合併資料表發行項之間的邏輯記錄關聯性](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [指定合併資料表發行項的處理順序 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [將合併資料表發行項指定為僅限下載](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [指定不應該為合併發行項追蹤刪除 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [指定合併發行項的衝突追蹤與解決層級](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [指定合併發行項解析程式](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [指定合併發行項的互動式衝突解決方法](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
