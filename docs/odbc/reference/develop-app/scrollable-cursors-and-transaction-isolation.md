---
description: 可捲動的資料指標和交易隔離
title: 可滾動的資料指標和交易隔離 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 790b2d0c4d80c821645c3a4360d1295cc55a8a4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476500"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可捲動的資料指標和交易隔離
下表列出管理變更可見度的因素。  
  
|進行的變更：|可見度取決於：|  
|----------------------|----------------------------|  
|資料指標|資料指標類型，資料指標執行|  
|相同交易中的其他語句|資料指標類型|  
|其他交易中的語句|資料指標類型，交易隔離等級|  
  
 下圖顯示這些因素。  
  
 ![管理變更的可見性之因數](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表摘要說明每個資料指標類型偵測本身所做的變更、本身交易中的其他作業，以及其他交易的能力。 後者變更的可見度取決於資料指標類型，以及包含資料指標之交易的隔離等級。  
  
|資料指標 type\action|Self|自己<br /><br /> Txn|其他<br /><br /> Txn<br /><br />  (RU [a] ) |其他<br /><br /> Txn<br /><br />  (RC [a] ) |其他<br /><br /> Txn<br /><br />  (RR [a] ) |其他<br /><br /> Txn<br /><br />  (S [a] ) |  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|靜態|||||||  
|插入|或許 [b]|否|否|否|否|否|  
|更新|或許 [b]|否|否|否|否|否|  
|刪除|或許 [b]|否|否|否|否|否|  
|索引鍵集導向的資料指標|||||||  
|插入|或許 [b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|刪除|或許 [b]|是|是|是|否|否|  
|動態|||||||  
|插入|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|刪除|是|是|是|是|否|否|  
  
 [a] 括弧中的字母表示包含資料指標之交易的隔離等級;其他交易 (的隔離等級) 不相關的變更。  
  
 RU：讀取未認可  
  
 RC：讀取認可  
  
 RR：可重複讀取  
  
 S： Serializable  
  
 [b] 取決於資料指標的實作為方式。 資料指標是否可以偵測到這類變更是透過 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項來回報。
