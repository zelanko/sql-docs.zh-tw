---
title: 建立資料庫 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a2af52bdfbb4e6e2a2f5b069ff4555fbce7315bc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034595"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>建立資料庫 (SQL Server 匯入和匯出精靈)
  使用**Create Database**頁面，即可定義新的資料庫，為目的地檔案。  
  
 這個頁面提供建立新資料庫之可用選項的子集。 若要檢視所有選項，請使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 若要深入了解這個精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解啟動精靈，選項和權限，才能成功執行精靈，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 為目的地 SQL Server 資料庫提供唯一的名稱。 當您命名此資料庫時，請確認有遵循 SQL Server 慣例。  
  
 **資料檔案名稱**  
 檢視資料檔的名稱。 這是從您在先前提供的資料庫名稱衍生的。  
  
 **記錄檔名稱**  
 檢視記錄檔的名稱。 這是從您在先前提供的資料庫名稱衍生的。  
  
 **初始大小 （資料檔）**  
 指定資料檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長 （資料檔）**  
 指出資料檔是否可以成長超過指定的初始大小。  
  
 **成長百分比 （資料檔）**  
 指定資料檔可以成長的百分比。  
  
 **成長大小 （資料檔）**  
 指定資料檔可以成長的大小 (以 MB 為單位)。  
  
 **初始大小 （記錄檔）**  
 指定記錄檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長 （記錄檔）**  
 指出記錄檔是否可以成長超過指定的初始大小。  
  
 **成長百分比 （記錄檔）**  
 指定記錄檔可以成長的百分比。  
  
 **成長大小 （記錄檔）**  
 指定記錄檔可以成長的大小 (以 MB 為單位)。  
  
  