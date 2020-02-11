---
title: 修改唯一的條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8bb3daf170e25abc9b346aeaedb4b835cae2dfdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68809924"
---
# <a name="modify-unique-constraints"></a>修改唯一的條件約束
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改唯一條件約束。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列條件修改 unique 條件約束：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>若要修改唯一條件約束  
  
1.  在 [物件總管]**** 中，以滑鼠右鍵按一下包含唯一條件約束的資料表，然後選取 [設計]****。  
  
2.  在 [資料表設計工具]**** 功能表中，按一下 [索引/索引鍵]****。  
  
3.  在 [索引/索引鍵]**** 對話方塊的 [選取的主/唯一索引鍵或索引]**** 底下，選取您想要編輯的條件約束。  
  
4.  完成下表中的動作：  
  
    |至|請依照下列步驟：|  
    |--------|------------------------|  
    |變更與條件約束有關的資料行|1) 在 [(一般)]**** 底下的方格中，按一下 [資料行]****，然後按一下屬性右邊的省略符號 **(...)**。<br /><br /> 2) 在 [索引資料行]**** 對話方塊中，指定索引的新資料行或排序次序，同時指定這兩者。|  
    |重新命名條件約束|在 **[識別]** 底下的方格中，於 **[名稱]** 方塊中輸入新的名稱。 確定新名稱不會與 [選取的主索引鍵/唯一索引鍵或索引]  清單中的名稱重複。|  
    |設定叢集選項|在 [資料表設計工具]**** 下的方格中，選取 [建立為叢集]****，然後從下拉式清單中，選擇 [是] 建立叢集索引，或選擇 [否] 建立非叢集索引。 每個資料表只能存在一個叢集索引。 如果叢集索引已經存在這個資料表中，您就必須清除原始索引的這項設定。|  
    |定義填滿因數|在 **[資料表設計工具]** 底下的方格中，展開 **[填滿規格]** 類別目錄，然後在 **[填滿因數]** 方塊中輸入 0 到 100 之間的整數。|  
  
5.  在 [檔案]  功能表上，按一下 [儲存 <資料表名稱>]   。  
  
##  <a name="TsqlProcedure"></a>**修改 unique 條件約束**  
  
 若要使用 Transact-SQL 來修改 UNIQUE 條件約束，您必須先刪除現有的 UNIQUE 條件約束，然後使用新的定義來重新建立。 如需相關資訊，請參閱 [Delete Unique Constraints](delete-unique-constraints.md) 及 [Create Unique Constraints](create-unique-constraints.md)。  
  
###  <a name="TsqlExample"></a>  
