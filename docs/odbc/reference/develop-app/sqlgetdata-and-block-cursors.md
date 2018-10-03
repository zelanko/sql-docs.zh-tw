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
manager: craigg
ms.openlocfilehash: a14c98f045fd974b404209cc998496dc5fa7193e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755521"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData**作業的單一資料列的單一資料行，而且無法擷取陣列，包含多個資料列的資料。 這是因為主要使用的**SQLGetData**是擷取組件中的 long 資料，而且沒有少量或沒有執行此動作一次多個資料列的原因。  
  
 若要使用**SQLGetData**使用區塊資料指標，應用程式第一次呼叫**SQLSetPos**若要將游標放在單一資料列。 然後它會呼叫**SQLGetData**中該資料列的資料行。 不過，此行為是選擇性的。 若要判斷驅動程式是否支援使用**SQLGetData**應用程式會使用區塊資料指標，呼叫**SQLGetInfo** SQL_GETDATA_EXTENSIONS 選項。
