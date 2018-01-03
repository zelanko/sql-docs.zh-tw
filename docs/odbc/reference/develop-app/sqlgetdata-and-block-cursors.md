---
title: "SQLGetData 和區塊資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12b3c2dc5693f141f24b9209a12923b18a9859e5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData**單一資料列的單一資料行上運作，且無法擷取陣列，其中包含來自多個資料列的資料。 這是因為主要使用的**SQLGetData**是擷取組件中的 long 資料，而且沒有少量或沒有執行此工作一次一個以上的資料列的原因。  
  
 若要使用**SQLGetData**使用區塊資料指標，應用程式第一次呼叫**SQLSetPos**以將游標放在單一資料列。 然後它會呼叫**SQLGetData**中該資料列的資料行。 不過，這種行為是選擇性的。 若要判斷驅動程式是否支援使用**SQLGetData**應用程式會使用區塊資料指標，呼叫**SQLGetInfo** SQL_GETDATA_EXTENSIONS 選項。
