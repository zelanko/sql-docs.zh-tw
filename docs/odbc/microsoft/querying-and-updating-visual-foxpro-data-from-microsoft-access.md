---
title: 從微軟訪問查詢和更新可視化 FoxPro 數據 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11b49ed099ba29d0e7e013af99a8ad96ca6825c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292868"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>從 Microsoft Access 查詢和更新 Visual FoxPro 資料
您可以使用「連結表」選項從 Microsoft Access 資料庫查詢和更新儲存在 Visual FoxPro 資料庫中的數據。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>將 Visual FoxPro 資料庫連結到 Microsoft 存取資料庫  
  
1.  打開 Microsoft 訪問資料庫。  
  
2.  在"表"選項卡中,按一下"新建"。  
  
3.  在"新建表"對話框中,選擇"連結表"並按兩下"確定"。  
  
4.  在「連結對話框」 中,在「類型檔案」 清單中選擇 ODBC 資料庫。  
  
5.  在 SQL 資料源對話方塊中,選擇連接到要查詢的 Visual FoxPro 資料的資料源,然後單擊"確定"  
  
6.  在"鏈接表"對話框中,選擇要查詢和更新的表,然後單擊"確定"。 連結的 Visual FoxPro 表顯示在 Microsoft 訪問資料庫的「表」選項卡中。  
  
 您現在可以使用 Microsoft Access 查詢和更新連結的 Visual FoxPro 表中的數據。 對連結數據所做的更改將發送回 Visual FoxPro 資料來源。  
  
 如果您不希望在 Microsoft 存取中所做的更改影響 Visual FoxPro 資料來源的資料,請參閱[將可視化 FoxPro 資料匯入 Microsoft 存取](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
