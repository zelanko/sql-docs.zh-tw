---
title: 將 Visual FoxPro 資料匯入 Microsoft Access |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085537"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>將 Visual FoxPro 資料匯入 Microsoft Access 中
您可以使用 [匯入] 選項，將儲存在 Visual FoxPro 資料庫中的資料匯入至 Microsoft Access 資料庫。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>將 Visual FoxPro 資料匯入 Microsoft Access 資料庫  
  
1.  開啟 Microsoft Access 資料庫。  
  
2.  從 [檔案] 功能表中，選擇 [取得外部資料] 然後 [匯入]。  
  
3.  在 [匯入] 對話方塊的 [檔案類型] 清單中，選取 [ODBC 資料庫]。  
  
4.  在 [SQL 資料來源] 對話方塊中，選取連接到您要查詢之 FoxPro 資料的 Visual FoxPro 資料來源，然後按一下 [確定]。  
  
5.  在 [匯入物件] 對話方塊中，選取您要匯入的一或多個資料表，然後按一下 [確定]。 您匯入之 Visual FoxPro 資料表的名稱會顯示在 Microsoft Access 資料庫的 [資料表] 索引標籤中。  
  
 您現在可以使用 Microsoft Access 來操作匯入之 Visual FoxPro 資料表中的資料。 您匯入的資料是儲存在 Visual FoxPro 中的資料快照集;您對匯入資料所做的變更不會傳送回 Visual FoxPro 資料來源。  
  
 如果您想要在 Microsoft Access 變更 Visual FoxPro 資料來源上的資料所做的變更，請參閱[從 Microsoft Access 查詢和更新 Visual Foxpro 資料](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
