---
description: 唯讀狀態 (Excel 驅動程式)
title: 唯讀狀態 (Excel 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 04a0c5d0cb2c9932d30c0edb900169d8c5e5f82b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340384"
---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 (Excel 驅動程式)
使用 Microsoft Excel 驅動程式時，資料來源資料表預設會以唯讀方式開啟，而且一次只能由一個使用者開啟。 不過，雖然資料表具有唯讀狀態，但應用程式可以執行 Microsoft Excel 資料表的插入和更新。  
  
 當應用程式透過 Microsoft Excel 驅動程式在 Microsoft Excel 資料上執行 [另存新檔] 命令時，應用程式應該建立新的資料表，並插入要儲存到新資料表中的資料。 在資料表的附加中插入結果。 在關閉並重新開啟之前，無法在資料表上執行其他作業。 當資料表關閉之後，就不能再執行後續的插入，因為資料表就是唯讀資料表。  
  
 使用 Microsoft Excel 驅動程式時，您可以更新值，但無法從以 Microsoft Excel 試算表為基礎的資料表中刪除資料列，因此 Microsoft Excel 驅動程式不會將更新視為正式支援。
