---
title: 唯讀狀態 （Excel 驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17425e76814a8397b9d2e6167248f35e52ac6cfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697436"
---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 (Excel 驅動程式)
使用 Microsoft Excel 驅動程式時，資料來源資料表會以唯讀模式開啟的預設值，，和只有一位使用者可以開啟一次。 即使資料表有唯讀狀態，不過，應用程式可以執行插入和更新的 Microsoft Excel 資料表。  
  
 當應用程式透過 Microsoft Excel 驅動程式的 Microsoft Excel 資料上執行 [另存新檔] 命令時，應用程式應該建立新的資料表，並將資料儲存至新的資料表。 插入會導致附加至資料表。 任何其他作業可以不執行在資料表上，直到它已關閉並重新開啟。 一旦關閉資料表，因為資料表則是唯讀的資料表，所以無法執行任何後續的 insert。  
  
 您可使用 Microsoft Excel 驅動程式時，更新的值，但無法刪除資料列，從資料表為基礎的 Microsoft Excel 試算表中，因此更新較不正式支援的 Microsoft Excel 驅動程式。
