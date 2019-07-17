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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107403"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData**作業的單一資料列的單一資料行，而且無法擷取陣列，包含多個資料列的資料。 這是因為主要使用的**SQLGetData**是擷取組件中的 long 資料，而且沒有少量或沒有執行此動作一次多個資料列的原因。  
  
 若要使用**SQLGetData**使用區塊資料指標，應用程式第一次呼叫**SQLSetPos**若要將游標放在單一資料列。 然後它會呼叫**SQLGetData**中該資料列的資料行。 不過，此行為是選擇性的。 若要判斷驅動程式是否支援使用**SQLGetData**應用程式會使用區塊資料指標，呼叫**SQLGetInfo** SQL_GETDATA_EXTENSIONS 選項。
