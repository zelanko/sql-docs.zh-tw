---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4841d8d923ff73d187569df3d7f9e29daf0f4e48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107403"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData**會在單一資料列的單一資料行上運作，而且無法提取包含來自多個資料列之資料的陣列。 這是因為**SQLGetData**的主要用途是在元件中提取長資料，而不需要一次為一個以上的資料列執行此動作。  
  
 若要搭配使用**SQLGetData**與區塊資料指標，應用程式會先呼叫**SQLSetPos** ，將游標放在單一資料列上。 然後，它會針對該資料列中的資料行呼叫**SQLGetData** 。 不過，此行為是選擇性的。 若要判斷驅動程式是否支援使用具有區塊資料指標的**SQLGetData** ，應用程式會使用 SQL_GETDATA_EXTENSIONS 選項來呼叫**SQLGetInfo** 。
