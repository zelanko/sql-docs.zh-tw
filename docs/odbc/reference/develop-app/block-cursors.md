---
title: 塊游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306349"
---
# <a name="block-cursors"></a>區塊資料指標
許多應用程式花費大量時間通過網路傳輸數據。 這一時間的一部分實際上用於將數據帶入整個網路,其中一部分用於網路開銷,例如驅動程式調用請求一行數據。 如果應用程式有效地使用塊或*胖**游標,* 則可以減少後一時間,因為*塊*或胖游標一次可以返回多個行。  
  
 應用程式始終可以選擇使用塊游標。 在一次只能提取一行的數據源上,必須在驅動程式中類比塊游標。 這可以通過執行多個單行提取來實現。 雖然這不太可能帶來任何性能提升,但它為應用程式提供了機會。 然後,隨著 DBMS 本機實現塊游標以及與這些 DBMS 關聯的驅動程式公開它們,此類應用程式的性能將提升。  
  
 在具有區塊游標的單抽取中傳回的行為*行集*。 重要的是不要將行集與結果集混淆。 結果集保存在數據源中,而行集則保存在應用程式緩衝區中。 當結果集是固定的時,行集不是 - 每次提取一組新的行時,都會更改位置和內容。 正如單行遊標(如傳統的 SQL 只向前游標)指向目前的行一樣,區塊游標指向行集,這可視為*目前的行*。  
  
 要在提取多行時對一行執行操作,應用程式必須首先指示哪行是當前行。 呼叫**SQLGetData**和定位更新和刪除語句需要當前行。 當塊游標首次返回行集時,當前行是行集的第一行。 要更改當前行,應用程式將調用**SQLSetPos**或**SQLBulk 操作**(按書籤更新)。 下圖顯示了結果集、行集、當前行、行集游標和塊游標的關係。 有關詳細資訊,請參閱在本部分後面的[中使用塊游標](../../../odbc/reference/develop-app/using-block-cursors.md),以及[使用 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)[定位更新和刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和更新數據。  
  
 ![提取下一個、上一個、第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 游標是否是塊游標,與游標是否可滾動無關。 例如,報表應用程式中的大部分工作都用於檢索和列印行。 因此,它將以最快速度使用僅轉發塊游標。 它使用僅轉發游標來避免可滾動游標的費用,使用塊游標來減少網路流量。  
  
 此章節包含下列主題。  
  
-   [繫結資料行以搭配使用區塊資料指標](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [資料列狀態陣列](../../../odbc/reference/develop-app/row-status-array.md)
