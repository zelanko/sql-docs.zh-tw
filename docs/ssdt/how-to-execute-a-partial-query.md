---
title: 如何：執行部分查詢 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2f7861e3ef232dd3f244c9c325468e6ba4d51d16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929616"
---
# <a name="how-to-execute-a-partial-query"></a>如何：執行部分查詢
Transact\-SQL 編輯器可讓您反白顯示指令碼的特定區段，並且將它執行成單一查詢。 這樣可以讓您輕鬆地偵錯複雜查詢的區段。  
  
> [!WARNING]  
> 下列程序使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-partially-execute-a-query"></a>若要部分執行查詢  
  
1.  在 [SQL Server 物件總管]  中，按兩下 [檢視表]  下的 **PerishableFruits**，在 Transact\-SQL 編輯器中打開它。  
  
2.  反白顯示程式碼中的 `SELECT p.Id, p.Name FROM dbo.Product p` 區段，按一下滑鼠右鍵選取 [執行查詢]  。  
  
3.  請注意，`Products` 資料表中具有指定之欄位的所有資料列傳回於 [結果]  窗格中。  
  
