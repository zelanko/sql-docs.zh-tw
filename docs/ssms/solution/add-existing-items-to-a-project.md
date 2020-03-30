---
title: 將現有的項目加入至專案
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9f17139dfae9a04fe71c8b4d493b0be24d875c4b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241886"
---
# <a name="add-existing-items-to-a-project"></a>將現有的項目加入至專案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
請將新的項目加入專案中，來延伸應用程式功能。 現有項目可以是查詢或其他檔案。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 有兩種專案類型： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案和 Analysis Services 指令碼專案。 專案類型決定了可以加入專案中的查詢檔。 例如，您可以將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢 (副檔名是 .sql 的檔案) 加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案中，但您不能將它加入 Analysis Services 指令碼專案中。 若要使副檔名與專案類型相關聯，請參閱 [如何：使副檔名與程式碼編輯器相關聯](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>將現有的查詢或其他檔案加入專案中  
  
1.  在 [方案總管] 中，選取一個目標專案。  
  
2.  在 [專案]  功能表上，按一下 [新增現有項目]  。  
  
    **Look in**  
    從此清單中找出要加入專案的檔案或資料夾。 針對 XML Web 服務和 ASP.NET Web 應用程式，這些檔案是位於 Web 伺服器上。  
  
    **桌面**  
    顯示位於桌面上的檔案和資料夾。  
  
    **我的專案**  
    顯示位於預設 [我的專案]  位置處的檔案和資料夾。  
  
    **我的電腦**  
    顯示 [我的電腦]  資料夾的內容。  
  
    **檔案名稱**  
    使用此選項來篩選所顯示的檔案和資料夾。 輸入要篩選的完整或部份檔案名稱；使用星號 (`*`) 作為萬用字元。  
  
    > [!NOTE]  
    > 在 [檔案名稱]  方塊中輸入 URL 或網路路徑，導覽至 Web 和網路位置。 例如， **`https://mywebsite`** 會顯示在 mywebsite Web 位置上的可用檔案，而 **\\\myserver\myshare** 則會顯示在 myserver 的 myshare 位置上的可用檔案。  
  
    **檔案類型**  
    使用此選項根據副檔名篩選檔案。 每個產品都會列出最常用之檔案類型的預設篩選。  
  
    **加入**  
    使用此下拉式按鈕將項目加入專案中並在預設編輯器中開啟項目。  
  
    -   **加入**  
  
        將現有的項目複製到磁碟上的專案資料夾，並將項目加入方案總管中所選取的專案之下。 對項目所做的任何變更不會反映到位於原始位置的項目中。 這是此檔案類型的預設編輯器。  
  
    -   **加入做為連結**  
  
        將選取的檔案加入專案中並以該檔案類型的預設編輯器開啟它。 此選項會開啟原始選取的檔案，但不會將檔案複製到專案資料夾。  
  
3.  如果您要加入查詢檔，連接對話方塊會提示您指定查詢的連接。 如果不要將連接關聯於這項查詢，您可以在連接對話中，按一下 [取消]  。  
  
4.  此時檔案會加入專案的 [查詢]  或 [其他檔案]  資料夾中。  
  
## <a name="see-also"></a>另請參閱  
[方案總管](../../ssms/solution/solution-explorer.md)  
[將新項目加入專案](../../ssms/solution/add-new-items-to-a-project.md)  
[移除或刪除項目或專案](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
