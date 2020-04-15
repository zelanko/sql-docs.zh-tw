---
title: 鍵集驅動游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306203"
---
# <a name="keyset-driven-cursors"></a>索引鍵集導向的資料指標
鍵集驅動的游標位於靜態游標和動態游標之間,用於檢測更改。 如同靜態資料指標，它不一定會偵測結果集的成員資格和順序變更。 與動態游標一樣,它確實檢測結果集中行值的更改(受事務的隔離級別的約束,由SQL_ATTR_TXN_ISOLATION連接屬性設置)。  
  
 打開鍵集驅動的游標時,它會保存整個結果集的鍵;這將修復結果集的明顯成員身份和順序。 當游標滾動到結果集時,它使用此*鍵集中*的鍵檢索每行的當前數據值。 例如,假設鍵集驅動的游標獲取一行,然後另一個應用程式更新該行。 如果游標重新提取行,則它看到的值是新的值,因為它使用其鍵重新提取行。 因此,鍵集驅動的游標始終檢測自己和其他人所做的更改。  
  
 當游標嘗試檢索已刪除的行時,此行在結果集中顯示為「孔」:該行的鍵存在於鍵集中,但該行不再存在於結果集中。 如果更新了行中的鍵值,則該行將被視為已刪除並插入,因此此類行也會在結果集中顯示為孔。 雖然鍵集驅動的游標始終可以檢測其他人刪除的行,但它可以選擇從密鑰集中刪除自己刪除的行的鍵。 執行此操作的鍵集驅動游標無法檢測到它們自己的刪除。 特定鍵集驅動的游標是否檢測到其自己的刪除是通過**SQLGetInfo**中的SQL_STATIC_SENSITIVITY選項報告的。  
  
 其他人插入的行永遠不會對鍵集驅動的游標可見,因為鍵集中中不存在這些行的鍵。 但是,鍵集驅動的游標可以選擇將其插入自己的行的鍵添加到鍵集中。 執行此操作的鍵集驅動游標可以檢測自己的插入。 特定鍵集驅動的游標是否檢測到其自己的插入是通過**SQLGetInfo**中的SQL_STATIC_SENSITIVITY選項報告的。  
  
 SQL_ATTR_ROW_STATUS_PTR語句屬性指定的行狀態陣列可以包含任何行的SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO或SQL_ROW_ERROR。 它返回SQL_ROW_UPDATED、SQL_ROW_DELETED或SQL_ROW_ADDED,用於它檢測到的更新、刪除或插入的行。  
  
 鍵集驅動的遊標通常是通過創建一個臨時表實現的,該表包含結果集中每行的鍵。 由於游標還必須確定行是否已更新,因此此表通常還包含包含行版本控制資訊的列。  
  
 要滾動原始結果集,鍵集驅動的游標將在臨時表上打開靜態游標。 若要檢索原始結果集中的行,游標首先從臨時表中檢索相應的鍵,然後檢索該行的當前值。 如果使用塊游標,游標必須檢索多個鍵和行。
