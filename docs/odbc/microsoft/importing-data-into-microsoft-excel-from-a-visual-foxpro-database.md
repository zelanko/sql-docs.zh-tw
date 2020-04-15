---
title: 從視覺化 FoxPro 資料庫將資料匯入 Microsoft Excel |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287668"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>將資料從 Visual FoxPro 資料庫匯入 Microsoft Excel 中
如果您已為其定義了數據源,則可以將 Visual FoxPro 資料導入 Microsoft Excel 工作表。 有關建立 Visual FoxPro 資料來源的資訊,請參閱[從 Microsoft Excel 存取視覺化 FoxPro 資料來源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>將 Visual FoxPro 資料匯入 Microsoft Excel 工作表  
  
1.  打開 Microsoft Excel 電子表格。  
  
2.  在「數據」功能表中,選擇「獲取外部數據」。 打開微軟查詢。  
  
3.  在「選擇數據源」對話框中,選擇 Visual FoxPro 資料源,然後單擊"使用"  
  
4.  如果數據來源存取的資料庫包含表,請從「添加表」對話框中選擇一個表。 Microsoft 查詢在查詢設計器的上半部分顯示添加的表。  
  
    > [!NOTE]  
    >  "擁有者"清單在此對話框中不可用,因為驅動程式不支援所有者。 資料庫清單不可用,因為驅動程式不支援數據來源中的多個資料庫。  
  
5.  通過將欄位從錶拖動到設計器的下半部分,為查詢選擇欄位。  
  
6.  關閉微軟查詢。 您選擇的數據將匯入到 Microsoft Excel 電子表格中。
