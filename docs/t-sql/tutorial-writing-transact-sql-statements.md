---
title: "教學課程： 撰寫 TRANSACT-SQL 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c42fed70b1335a48bcc219682d5be5e4010e0e5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="tutorial-writing-transact-sql-statements"></a>教學課程：撰寫國際性通用的 Transact-SQL 陳述式
歡迎使用「撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式」教學課程。 本教學課程的主要對象是撰寫 SQL 陳述式的新手， 會透過檢閱一些建立資料表及插入資料的基本陳述式，協助新手上路。 本教學課程採用 [!INCLUDE[tsql](../includes/tsql-md.md)]，是 SQL 標準的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 實作。 本教學課程的目的是用來概述 [!INCLUDE[tsql](../includes/tsql-md.md)] 語言，而非用來取代 [!INCLUDE[tsql](../includes/tsql-md.md)] 類別。 在本教學課程中的陳述式是有意經過簡化的，並無意呈現一般實際資料庫中所遇到的複雜問題。  
  
>**注意︰** 如果您是初學者，可能會覺得使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 反而比撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式更簡單。  
  
## <a name="finding-more-information"></a>尋找詳細資訊  
若要尋找任何特定陳述式的詳細資訊，請在《SQL Server 線上叢書》中依名稱搜尋陳述式，或是使用 [內容] 瀏覽 [Transact-SQL 參考 &#40;Database Engine&#41;](../t-sql/transact-sql-reference-database-engine.md) 底下依字母順序排列的 1,800 個語言元素。 此外，搜尋與您有興趣的主題內容相關的關鍵字，也是另一種找出資訊的不錯方式。 例如，您想要知道如何傳回一部分的日期 (如月份)，您可以搜尋 **dates [SQL Server]** 的索引，然後選取 **dateparts**， 即會帶您前往 [DATEPART &#40;Transact-SQL&#41;](../t-sql/functions/datepart-transact-sql.md) 主題。 例如若要找出如何使用字串，您可以搜尋**字串函數**， 即會帶您前往[字串函數 &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md) 主題。  
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程會示範如何建立資料庫、在資料庫中建立資料表、插入資料至資料表、更新資料、讀取資料、刪除資料，然後刪除資料表。 您將建立檢視和預存程序，並將使用者設定到資料庫及資料。  
  
本教學課程分成三個課程：  
  
[第 1 課：建立資料庫物件](../t-sql/lesson-1-creating-database-objects.md)  
在這一課，您會建立資料庫、在資料庫中建立資料表、插入資料至資料表、更新資料以及讀取資料。  
  
[第 2 課：設定資料庫物件的權限](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)  
在這一課，您會建立登入及使用者， 也會建立檢視和預存程序，然後將使用者權授與預存程序。  
  
[第 3 課：刪除資料庫物件](../t-sql/lesson-3-deleting-database-objects.md)  
在這一課，您會移除資料的存取、從資料表中刪除資料、刪除資料表，最後刪除資料庫。  
  
## <a name="requirements"></a>需求  
為了完成本教學課程，您並不需要精通 SQL 語言，但必須了解基本資料庫概念 (如資料表)。 在進行本教學課程期間，您將建立資料庫以及建立 Windows 使用者。 這些工作需要高層權限，因此您必須以系統管理員的身份登入電腦。  
  
另外，系統必須有安裝下列程式：  
  
-   任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-  [Transact-SQL](https://msdn.microsoft.com/library/mt238290.aspx)  
  

 
  
  
  


