---
description: SQLGetData 和區塊資料指標
title: SQLGetData 和區塊資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53358b2d4d8dfef1a5a820ed3943f07a584a595
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424490"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData** 會在單一資料列的單一資料行上運作，而且無法提取包含來自多個資料列之資料的陣列。 這是因為 **SQLGetData** 的主要用途是要在元件中提取長資料，而且很少或沒有理由一次對一個以上的資料列執行此動作。  
  
 若要搭配區塊資料指標使用 **SQLGetData** ，應用程式會先呼叫 **SQLSetPos** 將游標放在單一資料列上。 然後，它會針對該資料列中的資料行呼叫 **SQLGetData** 。 不過，此行為是選擇性的。 為了判斷驅動程式是否支援使用 **SQLGetData** 搭配區塊資料指標，應用程式會使用 SQL_GETDATA_EXTENSIONS 選項來呼叫 **SQLGetInfo** 。
