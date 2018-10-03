---
title: 建立副檔名與程式碼編輯器的關聯 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- file extensions [SQL Server]
- associating file extensions [SQL Server]
- Query Editor [SQL Server Management Studio], associating file extensions
ms.assetid: 193630f4-93de-4950-8f36-68702531f925
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cc6cd025c2e9c55d731e82c37040df512350620
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077518"
---
# <a name="associate-file-extensions-to-a-code-editor"></a>使副檔名與程式碼編輯器相關聯
  使副檔名與特定程式碼編輯器相關聯，可讓您在 Windows 檔案總管中按兩下檔案時，能以適當的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 程式碼編輯器開啟檔案。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]一般使用的副檔名 (例如 .sql 和 .mdx) 會在安裝期間產生關聯。 新的副檔名也必須在檔案系統中與 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 相關聯。 您可以使用此功能，開啟以其他編輯器建立的檔案，或開啟已重新命名的檔案，例如重新命名為 .bak 的 .sql 檔案備份。  
  
 處理過程有兩個步驟。 先使副檔名與 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]相關聯，然後再使副檔名與特定程式碼編輯器相關聯。  
  
### <a name="to-associate-a-new-file-extension-with-sql-server-management-studio"></a>若要使新的副檔名與 SQL Server Management Studio 相關聯  
  
1.  在 **[開始]** 功能表上，指向 **[所有程式]**，再指向 **[附屬應用程式]**，然後按一下 **[Windows 檔案總管]**。  
  
2.  在 Windows 檔案總管的 **[工具]** 功能表中，按一下 **[資料夾選項]**。  
  
3.  在 **[資料夾選項]** 對話方塊的 **[檔案類型]** 索引標籤上，按一下 **[新增]**。  
  
4.  在 **[建立新副檔名]** 對話方塊的 **[副檔名]** 方塊中，輸入要與之相關聯的新副檔名，再按一下 **[確定]**。 請不要以句點為開頭輸入副檔名。  
  
5.  在 **[註冊的檔案類型]** 方塊中，按一下新的副檔名，再按 **[變更]**。  
  
6.  在 **[開啟方式]** 對話方塊中，按一下 **[SSMS – SQL Server Management Studio]**，再按一下 **[確定]**。  
  
7.  按一下 **[關閉]** ，以關閉 **[資料夾選項]** 對話方塊，然後再關閉 Windows 檔案總管。  
  
### <a name="to-associate-a-new-file-extension-with-a-code-editor-in-sql-server-management-studio"></a>若要使新的副檔名與 SQL Server Management Studio 的程式碼編輯器相關聯  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，於 **[工具]** 功能表按一下 **[選項]**。  
  
2.  在 **[選項]** 對話方塊中，按一下 **[文字編輯器]**，再按一下 **[副檔名]**。  
  
3.  在 **[副檔名]** 方塊中，輸入新的副檔名。  
  
4.  在 **[編輯器]** 方塊中，依序按一下要用來開啟此檔案類型的程式碼編輯器、 **[新增]** 及 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [Ssms 公用程式](../../ssms/ssms-utility.md)  
  
  
