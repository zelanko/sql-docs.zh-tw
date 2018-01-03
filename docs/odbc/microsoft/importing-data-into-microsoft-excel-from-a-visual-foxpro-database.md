---
title: "Visual FoxPro 資料庫中的 Microsoft Excel 將資料匯入 |Microsoft 文件"
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
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c1c452e99e0da8b000163c50643b8ce93efe73e8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro 資料庫中的 Microsoft Excel 將資料匯入
如果您已經為它定義的資料來源，您可以 Visual FoxPro 資料匯入您的 Microsoft Excel 工作表。 建立 Visual FoxPro 資料來源的相關資訊，請參閱[從 Microsoft Excel 中存取 Visual FoxPro 資料來源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 資料匯入到 Microsoft Excel 工作表  
  
1.  開啟 Microsoft Excel 試算表。  
  
2.  從 資料 功能表中，選擇 取得外部資料。 Microsoft 查詢隨即開啟。  
  
3.  在 選取資料來源 對話方塊中，選取 Visual FoxPro 資料來源，然後按一下 使用。  
  
4.  如果您的資料來源來存取資料庫所包含的資料表，請從 [加入資料表] 對話方塊中選取資料表。 Microsoft 查詢會顯示加入的資料表中的查詢設計工具的上半部。  
  
    > [!NOTE]  
    >  擁有者清單不可以使用此對話方塊，因為驅動程式不支援的擁有者。 資料庫清單不可以使用，因為驅動程式不支援多個資料庫中的資料來源。  
  
5.  選取查詢的欄位拖曳到資料表中較低的設計工具 的下半部。  
  
6.  關閉 Microsoft 查詢。 您選取的資料匯入 Microsoft Excel 試算表。
