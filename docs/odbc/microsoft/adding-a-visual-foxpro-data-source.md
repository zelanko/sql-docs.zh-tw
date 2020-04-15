---
title: 新增視覺化 FoxPro 資料來源 ( C) :微軟文件
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
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307139"
---
# <a name="adding-a-visual-foxpro-data-source"></a>新增 Visual FoxPro 資料來源
要從應用程式存取 Visual FoxPro 資料,您必須具有資料來源。 可以按照以下方式建立資料來源:  
  
-   在使用 ODBC 驅動程式的應用程式中,如 Microsoft ® Word、Microsoft Excel 或 Microsoft Access。  
  
-   在應用程式外部,使用Microsoft Windows ®95、微軟Windows 98或Microsoft Windows NT®/Windows 2000控制面板。  
  
 在系統上存在數據源後,每次要訪問 Visual FoxPro 數據時,都可以重用相同的數據源。 如果要造訪多個不同的資料庫或表,則可以為每個資料庫或目錄創建單獨的數據來源。  
  
 以下過程使用控制面板創建數據源。 有關如何從應用程式創建資料來源的詳細資訊,請參閱[從 Microsoft Office 訪問 Visual FoxPro 資料](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>新增視覺化 FoxPro 資料來源  
  
1.  在運行 Windows 2000 的電腦上,打開 Windows 控制面板並按兩下管理工具。  
  
2.  按兩下資料來源 (ODBC) 以打開 ODBC 資料來源管理員對話方塊。 此圖示在安裝 Visual FoxPro ODBC 驅動程式或任何 ODBC 驅動程式軟體後可用。  
  
    > [!NOTE]  
    >  如果您正在運行早期版本的 Windows,請打開 Windows 控制面板並按兩下 32 位元 ODBC 或 ODBC 以打開 ODBC 資料來源管理員對話方塊。  
  
3.  按一下 [加入]。  
  
4.  在"創建新資料源"對話框中,選擇Microsoft視覺化FoxPro驅動程式,然後單擊"完成"。  
  
5.  在[ODBC Visual FoxPro 安裝程式對話框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中,鍵入數據源名稱和說明,選擇資料庫類型,選擇資料庫或目錄,然後單擊"確定"  
  
     新的資料來源名稱顯示在 ODBC 資料來源管理員對話方塊的使用者 DSN 選項卡中的「使用者數據來源」 清單中。  
  
6.  按下「確定」以儲存新資料源並關閉 ODBC 資料來源管理員對話方塊。
