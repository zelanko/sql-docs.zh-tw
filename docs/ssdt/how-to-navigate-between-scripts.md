---
title: 在指令碼之間巡覽
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.editor.howto.navigate
ms.assetid: 8664bde5-86ff-4e8b-b5a6-af003316f6ad
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 910011609e928efe9180a3aa4f041aa063adbab4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241376"
---
# <a name="how-to-navigate-between-scripts"></a>如何：在指令碼之間巡覽

適用於離線開發的 Transact\-SQL 編輯器提供兩個有用且 Visual Studio 使用者所熟悉的巡覽工具：[移至定義] 和 [尋找所有參考]。 例如，您可以用滑鼠右鍵按一下資料表名稱，然後用 [尋找所有參考] 列出專案中資料表的所有參考。 您可以按兩下搜尋結果以移至特定的程式碼檔案。 在這個檔案中，您可以再次用滑鼠右鍵按一下資料表名稱，然後選擇 [移至定義] 回到資料表定義。  
  
> [!WARNING]  
> 下列程序使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-navigate-between-scripts"></a>若要在指令碼之間巡覽  
  
1.  展開 [方案總管] 中的 [函數] 資料夾，然後按兩下 [GetProductsBySupplier.sql]。  
  
2.  以滑鼠右鍵按一下這行程式碼中的 `Products`，然後選取 [移至定義]   
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql 隨即自動開啟，顯示 `Products` 類型定義的位置。  
  
4.  回到 GetProductsBySupplier.sql。 這次為 `Products` 選取關聯式功能表中的 [尋找所有參考]。 在 [尋找符號結果]  窗格中，您會看到 `Products` 資料表參考的位置清單。 按兩下任何的搜尋結果，會將您帶到參考的位置。  
  
