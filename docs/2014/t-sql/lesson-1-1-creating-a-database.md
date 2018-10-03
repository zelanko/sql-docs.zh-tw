---
title: 建立資料庫 (教學課程) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c0353c89dbfc14032d33dfa49fa0c08e698cb5c0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098629"
---
# <a name="creating-a-database-tutorial"></a>建立資料庫 (教學課程)
  和許多 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式一樣，CREATE DATABASE 陳述式也有一個必要參數，那就是資料庫的名稱。 CREATE DATABASE 另外還有許多選擇性參數，例如，要用來放置資料庫檔案的磁碟位置。 當您執行 CREATE DATABASE 但未指定任何選擇性參數時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 多半會使用這些參數的預設值。 這個教學課程使用的選擇性語法參數非常少。  
  
### <a name="to-create-a-database"></a>若要建立資料庫  
  
1.  在 [查詢編輯器] 視窗中，輸入下列程式碼 (但不要執行)：  
  
    ```  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  使用指標選取 `CREATE DATABASE`這兩個字，然後按 **F1**鍵。 這時應該會開啟《SQL Server 線上叢書》中的＜CREATE DATABASE＞主題。 您可以利用這種方式找到 CREATE DATABASE 以及在這個教學課程中所使用之其他陳述式的完整語法。  
  
3.  在 [查詢編輯器] 中按 **F5** ，執行陳述式並建立名為 `TestData`的資料庫。  
  
 當您建立資料庫時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會建立 **model** 資料庫的複本，並且將此複本重新命名為資料庫的名稱。 除非您在選擇性參數中指定了非常大的資料庫初始大小，否則這項作業應該只需要幾秒鐘的時間。  
  
> [!NOTE]  
>  如果在單一批次中提交了一個以上的陳述式，可用關鍵字 GO 來分隔陳述式； 如果批次中只包含一個陳述式，則 GO 可有可無。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立資料表&#40;教學課程&#41;](lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
