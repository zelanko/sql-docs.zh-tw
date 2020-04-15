---
title: 將可視化 FoxPro 資料匯入微軟訪問 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90ac16bbdbaf7f4dd29e14e66cf5b9dc666057f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302441"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>將 Visual FoxPro 資料匯入 Microsoft Access 中
您可以使用「導入」選項將儲存在 Visual FoxPro 資料庫中的數據匯入到 Microsoft Access 資料庫中。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>將 Visual FoxPro 資料匯入 Microsoft 存取資料庫  
  
1.  打開 Microsoft 訪問資料庫。  
  
2.  從"檔案"功能表中,選擇"獲取外部數據,然後導入"。  
  
3.  在「導入」對話框中,在「類型檔」清單中選擇 ODBC 資料庫。  
  
4.  在 SQL 資料源對話方塊中,選擇連接到要查詢的 FoxPro 資料的 Visual FoxPro 資料來源,然後按一下" 確定"  
  
5.  在「導入物件」對話框中,選擇要導入的一個或多個表,然後單擊"確定"。 您匯入的 Visual FoxPro 表的名稱將顯示在 Microsoft Access 資料庫的「表」選項卡中。  
  
 您現在可以使用 Microsoft Access 操作導入的 Visual FoxPro 表中的數據。 您導入的數據是存儲在 Visual FoxPro 中的數據的快照;對導入的數據所做的更改不會發送回 Visual FoxPro 資料來源。  
  
 如果您希望在 Microsoft Access 中進行更改以更改 Visual FoxPro 資料來源上的資料,請參閱[從 Microsoft Access 查詢和更新 Visual FoxPro 資料](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
