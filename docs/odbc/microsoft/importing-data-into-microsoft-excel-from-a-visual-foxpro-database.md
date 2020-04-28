---
title: 從 Visual FoxPro 資料庫將資料匯入 Microsoft Excel |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287668"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>將資料從 Visual FoxPro 資料庫匯入 Microsoft Excel 中
如果您已為其定義了資料來源，則可以將 Visual FoxPro 資料匯入至 Microsoft Excel 工作表。 如需建立 Visual FoxPro 資料來源的詳細資訊，請參閱[從 Microsoft Excel 存取 Visual Foxpro 資料來源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>將 Visual FoxPro 資料匯入 Microsoft Excel 工作表  
  
1.  開啟 Microsoft Excel 試算表。  
  
2.  從 [資料] 功能表中，選擇 [取得外部資料]。 Microsoft Query 隨即開啟。  
  
3.  在 [選取資料來源] 對話方塊中，選取一個 Visual FoxPro 資料來源，然後按一下 [使用]。  
  
4.  如果資料來源存取的資料庫包含資料表，請從 [加入資料表] 對話方塊中選取資料表。 Microsoft Query 會在查詢設計工具的上半部顯示加入的資料表。  
  
    > [!NOTE]  
    >  因為驅動程式不支援擁有者，所以無法在此對話方塊中使用 [擁有者] 清單。 資料庫清單無法使用，因為此驅動程式不支援資料來源中的多個資料庫。  
  
5.  選取查詢的欄位，方法是將其從資料表拖曳至設計工具的下半部。  
  
6.  關閉 [Microsoft Query]。 您選取的資料會匯入到您的 Microsoft Excel 試算表。
