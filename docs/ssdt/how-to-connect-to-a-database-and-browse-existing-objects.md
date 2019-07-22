---
title: 如何：連線到資料庫及瀏覽現有物件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.connectionpicker.f1
ms.assetid: 9b331800-3806-4459-ac58-88cdc98124d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 49049fbbff2397f6492cac385b10c23a66d48a74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897328"
---
# <a name="how-to-connect-to-a-database-and-browse-existing-objects"></a>如何：連線到資料庫及瀏覽現有物件
資料庫管理員與開發人員經常需要連接到即時資料庫，設計或瀏覽其結構描述，並查詢其物件。 Visual Studio 的 [SQL Server 物件總管] 現在包含專用的 [SQL Server]  節點，在這個節點下所有連接的 SQL Server 執行個體及其資料庫都依照與 SSMS 類似的階層分組。 連接的 SQL Server 執行個體可以是內部部署執行個體 (例如執行中的 SQL Server 2008 伺服器)，或是外部部署 SQL Azure 執行個體。  
  
下列程序假設您已經安裝 AdventureWorks 範例資料庫。 使用 [CodePlex](https://msftdbprodsamples.codeplex.com/) 尋找及安裝不同 SQL Server 版本適用的範例資料庫。 如有需要，您也可以依照下列步驟，使用伺服器中現有的資料庫。  
  
### <a name="to-connect-to-a-database-instance"></a>若要連接到資料庫執行個體  
  
1.  在 Visual Studio 中，請確定已開啟 [SQL Server 物件總管]  。 如果沒有開啟，請按一下 [檢視]  功能表，然後選取 [SQL Server 物件總管]  。  
  
2.  以滑鼠右鍵按一下 [SQL Server 物件總管]  中的 [SQL Server]  節點，然後選取 [加入 SQL Server]  。  
  
3.  在 **[連接至伺服器]** 對話方塊的 **[伺服器名稱]** 方塊中，輸入要連接的伺服器執行個體名稱，提供您的認證，然後按一下 **[連接]** 。  
  
4.  在 [SQL Server 物件總管]  中，展開伺服器執行個體底下的 [資料庫]  節點。 您會看到所有位於此伺服器執行個體的資料庫都加到這個 **[資料庫]** 節點底下。  
  
5.  展開 [AdventureWorks]  (或另一個資料庫) 節點。 您會發現所有資料庫實體都依照與 SQL Server Management Studio 類似的階層分組。  
  
