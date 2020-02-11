---
title: 區塊資料指標 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118823"
---
# <a name="block-cursors"></a>區塊資料指標
許多應用程式會花大量時間將資料帶入網路上。 在這段時間內，實際上是花在網路上的資料，而其中一部分是花在網路負擔上，例如驅動程式對要求資料列所做的呼叫。 如果應用程式有效率地使用*區塊（* 或*fat）* 資料*指標（* 可以一次傳回一個以上的資料列），則可以減少後者的時間。  
  
 應用程式一律具有使用區塊資料指標的選項。 在一次只能提取一個資料列的資料來源上，必須在驅動程式中模擬區塊資料指標。 這可以藉由執行多個單一資料列提取來完成。 雖然這不太可能會提供任何效能提升，但它會為應用程式開啟商機。 如此一來，這類應用程式將會隨著 Dbms 以原生方式執行區塊資料指標，以及與這些 Dbms 相關聯的驅動程式公開它們，  
  
 在具有區塊資料指標的單一提取中傳回的資料列，稱為資料列*集*。 請務必將資料列集與結果集混淆。 結果集會保留在資料來源，而資料列集則是保留在應用程式緩衝區中。 當結果集是固定的時，資料列集不會在每次提取新的資料列集時變更位置和內容。 就像是傳統 SQL 順向資料指標之類的單一資料列資料指標，會指向目前的資料列，區塊游標會指向資料列集，這可視為目前的資料*列*。  
  
 若要在提取多個資料列時執行在單一資料列上運作的作業，應用程式必須先指出哪一個資料列是目前的資料列。 呼叫**SQLGetData**和定位 update 和 delete 語句時，需要目前的資料列。 當區塊資料指標第一次傳回資料列集時，目前的資料列就是資料列集的第一個資料列。 若要變更目前的資料列，應用程式會呼叫**SQLSetPos**或**SQLBulkOperations** （以書簽更新）。 下圖顯示結果集的關聯性、資料列集、目前資料列、資料列集資料指標和區塊資料指標。 如需詳細資訊，請參閱本節稍後的[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)，以及使用 SQLSetPos 來[定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![提取下一個、上一個、第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 資料指標是否為區塊資料指標，與它是否為可滾動的無關。 例如，報表應用程式中的大部分工作都花在抓取和列印資料列。 因此，它會使用順向、區塊資料指標的速度最快。 它會使用順向資料指標來避免具有可滾動資料指標的費用，以及用來減少網路流量的區塊資料指標。  
  
 此章節包含下列主題。  
  
-   [繫結資料行以搭配使用區塊資料指標](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [資料列狀態陣列](../../../odbc/reference/develop-app/row-status-array.md)
