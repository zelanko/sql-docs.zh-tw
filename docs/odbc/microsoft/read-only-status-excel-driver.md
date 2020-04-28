---
title: 唯讀狀態（Excel 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304019"
---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 (Excel 驅動程式)
使用 Microsoft Excel 驅動程式時，資料來源資料表預設會以唯讀方式開啟，而且一次只能由一個使用者開啟。 不過，即使資料表具有唯讀狀態，應用程式還是可以執行 Microsoft Excel 資料表的插入和更新。  
  
 當應用程式透過 Microsoft Excel 驅動程式在 Microsoft Excel 上執行 [另存新檔] 命令時，應用程式應該建立新的資料表，並插入要儲存到新資料表中的資料。 將附加中的結果插入資料表。 無法在資料表上執行其他作業，直到它關閉並重新開啟為止。 一旦資料表關閉之後，就不會執行後續的插入作業，因為資料表是唯讀資料表。  
  
 使用 Microsoft Excel 驅動程式時，可以更新值，但無法從以 Microsoft Excel 試算表為基礎的資料表中刪除資料列，因此 Microsoft Excel 驅動程式不會將更新視為正式支援。
