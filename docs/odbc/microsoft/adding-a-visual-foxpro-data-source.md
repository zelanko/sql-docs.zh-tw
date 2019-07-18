---
title: 新增 Visual FoxPro 資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5203a7216faa008aade21c4e3e1dc54fc794461b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901436"
---
# <a name="adding-a-visual-foxpro-data-source"></a>新增 Visual FoxPro 資料來源
若要存取 Visual FoxPro 資料從您的應用程式，您必須使用資料來源。 您可以建立資料來源，如下所示：  
  
-   應用程式，例如 Microsoft® Word、 Microsoft Excel 或 Microsoft Access 中，會使用 ODBC 驅動程式。  
  
-   應用程式之外使用 Microsoft Windows® 95、windows Microsoft Windows 98 或 Microsoft Windows/Windows 2000 控制台。  
  
 您的系統上不存在的資料來源之後，您可以重複使用相同的資料來源每當您想要存取 Visual FoxPro 資料。 如果您有數個不同的資料庫或您想要存取的資料表，您可以建立個別的資料來源的每個資料庫或目錄。  
  
 下列程序會使用控制台中，以建立資料來源。 如需如何從應用程式中建立資料來源的詳細資訊，請參閱[從 Microsoft Office 存取 Visual FoxPro 資料](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>若要新增 Visual FoxPro 資料來源  
  
1.  在執行 Windows 2000 的電腦，開啟 Windows 控制台中，按兩下 系統管理工具。  
  
2.  按兩下資料來源 (ODBC) 以開啟 [ODBC 資料來源管理員] 對話方塊。 您已安裝 Visual FoxPro ODBC Driver 或任何 ODBC 驅動程式軟體之後，可以使用此圖示。  
  
    > [!NOTE]  
    >  如果您執行較早版本的 Windows，請開啟 Windows 控制台，然後按兩下 32 位元 ODBC 或 ODBC，開啟 ODBC 資料來源管理員 對話方塊。  
  
3.  按一下 [加入]。  
  
4.  在 [建立新的資料來源] 對話方塊中，選取 Microsoft Visual FoxPro 驅動程式，然後按一下 [完成]。  
  
5.  在  [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)輸入資料來源名稱和描述，選取資料庫類型、 資料庫或目錄中，選取，然後按一下 [確定]。  
  
     新的資料來源名稱會顯示在 [ODBC 資料來源管理員] 對話方塊中 [使用者 DSN] 索引標籤中的 [使用者資料來源] 清單中。  
  
6.  按一下 [確定] 以儲存新的資料來源並關閉 [ODBC 資料來源管理員] 對話方塊。
