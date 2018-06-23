---
title: '使用 irow:: Getcolumns |Microsoft 文件'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 37c7895a888852a8acb0b73a4b44e297e1ea3318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037445"
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
  **IRow**實作可允許以順向循序方式存取資料行。 您可以存取的資料列的單一呼叫中的所有資料行**irow:: Getcolumns**或呼叫**irow:: Getcolumns**多次，每次您存取數個資料列中的資料行。  
  
 多個呼叫**irow:: Getcolumns**不應該重疊。 例如，如果第一次呼叫**irow:: Getcolumns**擷取資料行 1、 2 和 3，第二次呼叫**irow:: Getcolumns**應該呼叫資料行 4、 5 和 6。 如果稍後呼叫**irow:: Getcolumns**重疊，狀態旗標 （DBCOLUMNACCESS 中的 dwstatus 欄位） 會設定為 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>另請參閱  
 [使用 IRow 擷取單一資料列](fetching-a-single-row-with-irow.md)  
  
  