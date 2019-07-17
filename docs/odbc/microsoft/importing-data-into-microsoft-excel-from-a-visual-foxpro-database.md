---
title: 資料匯入至 Microsoft Excel 中從 Visual FoxPro 資料庫 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65635132c5f98b0565391122877f2e3c0a6714
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085552"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>將資料從 Visual FoxPro 資料庫匯入 Microsoft Excel 中
如果您已經為其定義資料來源，您可以 Visual FoxPro 資料匯至您的 Microsoft Excel 工作表。 如需建立 Visual FoxPro 資料來源的資訊，請參閱[從 Microsoft Excel 存取 Visual FoxPro 資料來源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 資料匯入到 Microsoft Excel 工作表  
  
1.  開啟 Microsoft Excel 試算表。  
  
2.  從 [資料] 功能表中，選擇 [取得外部資料]。 Microsoft 查詢隨即開啟。  
  
3.  在 [選取資料來源] 對話方塊中，選取 Visual FoxPro 資料來源，然後按一下使用。  
  
4.  如果您的資料來源來存取資料庫所包含的資料表，請從 [加入資料表] 對話方塊中選取資料表。 Microsoft 查詢會顯示在上半部的查詢設計工具中加入的資料表。  
  
    > [!NOTE]  
    >  擁有者清單不可以使用此對話方塊，因為驅動程式不支援擁有者。 資料庫清單不可以使用，因為驅動程式不支援多個資料庫中的資料來源。  
  
5.  選取查詢的欄位拖曳到資料表中較低的設計工具 的下半部。  
  
6.  關閉 Microsoft 查詢。 您選取的資料會匯入 Microsoft Excel 試算表。
