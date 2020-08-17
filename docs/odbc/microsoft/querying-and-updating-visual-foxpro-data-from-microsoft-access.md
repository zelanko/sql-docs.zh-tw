---
description: 從 Microsoft Access 查詢和更新 Visual FoxPro 資料
title: 從 Microsoft Access 查詢和更新 Visual FoxPro 資料 |Microsoft Docs
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
ms.openlocfilehash: 82232cfa3c0bb32ccd87231f139e9aecf8342450
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340424"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>從 Microsoft Access 查詢和更新 Visual FoxPro 資料
您可以使用 [連結資料表] 選項，從 Microsoft Access 資料庫查詢並更新儲存在 Visual FoxPro 資料庫中的資料。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>將 Visual FoxPro 資料庫連結到 Microsoft Access 資料庫  
  
1.  開啟 Microsoft Access 資料庫。  
  
2.  在 [資料表] 索引標籤中，按一下 [新增]。  
  
3.  在 [新增資料表] 對話方塊中，選取 [連結資料表]，然後按一下 [確定]。  
  
4.  在 [連結] 對話方塊中，選取 [檔案類型] 清單中的 [ODBC Database]。  
  
5.  在 [SQL 資料來源] 對話方塊中，選取連接到您要查詢之 Visual FoxPro 資料的資料來源，然後按一下 [確定]。  
  
6.  在 [連結資料表] 對話方塊中，選取您要查詢和更新的資料表，然後按一下 [確定]。 連結的 Visual FoxPro 資料表會顯示在 Microsoft Access 資料庫的 [資料表] 索引標籤中。  
  
 您現在可以使用 Microsoft Access 來查詢及更新連結的 Visual FoxPro 資料表中的資料。 您對連結資料所做的變更會傳送回 Visual FoxPro 資料來源。  
  
 如果您不想讓 Microsoft Access 中的變更影響 Visual FoxPro 資料來源上的資料，請參閱將 [Visual Foxpro 資料匯入 Microsoft access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
