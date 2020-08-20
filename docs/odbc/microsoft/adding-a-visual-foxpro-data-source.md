---
description: 新增 Visual FoxPro 資料來源
title: 加入 Visual FoxPro 資料來源 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22ac95b51d543ca223148b169b53acb9c334d9f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494801"
---
# <a name="adding-a-visual-foxpro-data-source"></a>新增 Visual FoxPro 資料來源
若要從您的應用程式存取 Visual FoxPro 資料，您必須有資料來源。 您可以建立資料來源，如下所示：  
  
-   在使用 ODBC 驅動程式的應用程式中，例如 Microsoft® Word、Microsoft Excel 或 Microsoft Access。  
  
-   在您的應用程式外部，使用 Microsoft Windows®95、Microsoft Windows 98 或 Microsoft Windows NT®/Windows 2000 主控台。  
  
 當您的系統上有資料來源之後，您就可以在每次想要存取 Visual FoxPro 資料時重複使用相同的資料來源。 如果您有數個不同的資料庫或您想要存取的資料表，您可以為每個資料庫或目錄建立個別的資料來源。  
  
 下列程式會使用主控台來建立資料來源。 如需有關如何從應用程式建立資料來源的詳細資訊，請參閱 [從 Microsoft Office 存取 Visual FoxPro 資料](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>若要加入 Visual FoxPro 資料來源  
  
1.  在執行 Windows 2000 的電腦上開啟 Windows [控制台]，然後按兩下 [系統管理工具]。  
  
2.  按兩下 [資料來源] (ODBC) 開啟 [ODBC 資料來源管理員] 對話方塊。 當您安裝了 Visual FoxPro ODBC 驅動程式或任何 ODBC 驅動程式軟體之後，就可以使用此圖示。  
  
    > [!NOTE]  
    >  如果您執行的是舊版 Windows，請開啟 Windows [控制台]，然後按兩下 [32-位 ODBC] 或 [ODBC]，開啟 [ODBC 資料來源管理員] 對話方塊。  
  
3.  按一下 [加入]。  
  
4.  在 [建立新的資料來源] 對話方塊中，選取 [Microsoft Visual FoxPro 驅動程式]，然後按一下 [完成]。  
  
5.  在 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中，輸入資料來源名稱和描述、選取資料庫類型、選取資料庫或目錄，然後按一下 [確定]。  
  
     新的資料來源名稱會顯示在 [ODBC 資料來源管理員] 對話方塊的 [使用者 DSN] 索引標籤中的 [使用者資料來源] 清單中。  
  
6.  按一下 [確定] 儲存新的資料來源，然後關閉 [ODBC 資料來源管理員] 對話方塊。
