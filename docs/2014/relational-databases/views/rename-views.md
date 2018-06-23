---
title: 重新命名檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-views
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 84951488cfa1966468152f97b204ea6e0d08f92e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133384"
---
# <a name="rename-views"></a>重新命名檢視
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新命名檢視。  
  
> [!WARNING]  
>  如果您重新命名檢視，涉及該檢視的程式碼和應用程式都會失敗。 這些包含其他檢視、查詢、預存程序、使用者定義函數，以及用戶端應用程式。 注意，這些失敗會串聯。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **使用下列方法重新命名檢視：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After renaming a view](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 取得檢視的所有相依性的清單。 參考檢視的任何物件、指令碼或應用程式都必須修改，以反映檢視的新名稱。 如需詳細資訊，請參閱 [Get Information About a View](get-information-about-a-view.md)。 建議您卸除檢視，並使用新名稱重新建立檢視，而不要重新命名檢視。 透過重新建立檢視，可更新檢視中所參考之物件的相依性資訊。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 SCHEMA 的 ALTER 權限，或 OBJECT 的 CONTROL 權限，以及資料庫的 CREATE VIEW 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-view"></a>若要重新命名檢視  
  
1.  在 **[物件總管]** 中，展開資料庫，此資料庫包含您要重新命名的檢視，然後展開 **[檢視]** 資料夾。  
  
2.  以滑鼠右鍵按一下您要重新命名的檢視，然後選取 **[重新命名]**。  
  
3.  輸入檢視的新名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要重新命名檢視**  
  
 雖然您可以使用 **sp_rename** 變更檢視的名稱，但建議您刪除現有的檢視，然後使用新名稱重新建立檢視。  
  
 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql) 和 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)。  
  
##  <a name="FollowUp"></a> 待處理：重新命名檢視之後  
 確定參考檢視舊名稱的任何物件、指令碼和應用程式現在都使用新名稱。  
  
  
