---
description: 區塊資料指標
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dece0e3ecfc5ef4f3116361a202cfa2d10863ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476820"
---
# <a name="block-cursors"></a>區塊資料指標
許多應用程式花費大量的時間在網路上帶入資料。 這段時間的一部分是要實際將資料放在網路上，其中有一部分會花在網路額外負荷，例如驅動程式提出要求資料列的呼叫。 如果應用程式有效率地使用區塊或*fat、* 資料*指標（* 一次可能會傳回一個以上的*資料*列），則可以減少後者的時間。  
  
 應用程式一律具有使用區塊資料指標的選項。 對於一次只能提取一個資料列的資料來源，必須在驅動程式中模擬區塊資料指標。 這可以藉由執行多個單一資料列提取來完成。 雖然這不太可能提供任何效能提升，但是它會開啟應用程式的機會。 如此一來，這類應用程式將會隨著 Dbms 以原生方式執行區塊資料指標，且與 Dbms 相關聯的驅動程式公開這些資料指標  
  
 使用區塊資料指標在單一提取中傳回的資料列稱為資料列 *集*。 請務必將資料列集與結果集混淆。 結果集會在資料來源中維護，而資料列集則是在應用程式緩衝區中維護。 當結果集是固定的時，資料列集不會在每次提取新的資料列集時變更位置和內容。 就像是單一資料列資料指標，例如傳統 SQL 順向資料指標指向目前的資料列，區塊資料指標會指向資料列集，這可視為目前的資料 *列*。  
  
 若要在提取多個資料列時執行在單一資料列上運作的作業，應用程式必須先指出哪一個資料列是目前的資料列。 呼叫 **SQLGetData** 和定位 update 和 delete 語句時，需要目前的資料列。 當區塊資料指標首次傳回資料列集時，目前的資料列是資料列集的第一個資料列。 若要變更目前的資料列，應用程式會呼叫 **SQLSetPos** 或 **SQLBulkOperations** (，以) 的書簽進行更新。 下圖顯示結果集、資料列集、目前資料列、資料列集資料指標和區塊資料指標的關聯性。 如需詳細資訊，請參閱本節稍後的 [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)，以及 [定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) ，以及 [使用 SQLSetPos 來更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![提取下一個、上一個、第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 資料指標是否為區塊資料指標，與它是否為可滾動的無關。 例如，報表應用程式中的大部分工作都是花在抓取和列印資料列。 基於這個原因，它會使用順向、區塊資料指標的速度最快。 它會使用順向資料指標來避免可滾動資料指標的費用，以及封鎖資料指標以減少網路流量。  
  
 此章節包含下列主題。  
  
-   [繫結資料行以搭配使用區塊資料指標](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [資料列狀態陣列](../../../odbc/reference/develop-app/row-status-array.md)
