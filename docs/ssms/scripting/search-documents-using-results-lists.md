---
title: 使用結果清單搜尋文件
description: 了解如何搜尋和取代專案、解決方案或檔系統資料夾中所有內含檔案的文字。 相符項目會出現在 [尋找結果 1] 視窗中，您可按兩下相符項目來查看其所在字行。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fa62cc76deab4f40f7db63ebd119fc9cd227c72e
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122803"
---
# <a name="search-documents-using-results-lists"></a>使用結果清單搜尋文件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
   您可以利用 [尋找和取代]**** 對話方塊來搜尋和取代專案或方案或檔案系統資料夾中之所有檔案內的文字，即使尚未在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟它們，也是如此。 **[尋找和取代]** 對話方塊所執行之搜尋的相符項目會出現在 [尋找結果 1] 和 [尋找結果 2] 視窗中，可讓您檢視相符項目所在字行中的確實文字。  
  
### <a name="to-search-in-multiple-files"></a>在多個檔案中搜尋  
  
1.  在 **[編輯]** 功能表上，指向 **[尋找和取代]** ，再按一下 **[檔案中尋找]** 。  
  
2.  在 **[尋找目標]** 文字方塊中，輸入要搜尋的文字。  
  
3.  在 **[查詢]** 清單中，按一下 **[所有開啟的文件]** 、 **[目前的專案]** 或 **[整個方案]** ，或輸入目錄路徑。  
  
4.  在 **[檔案類型]** 清單中，選取列出的各組副檔名之一，或用分號分隔來輸入要搜尋之檔案類型的副檔名。 請利用 \*.\* 來搜尋 [查詢] 下拉式清單列出之目錄中的所有檔案。  
  
5.  選取其餘搜尋選項來改進搜尋的精確度。  
  
6.  按一下 **[尋找]** 來開始搜尋。  
  
 依預設，搜尋的相符項目會出現在 [尋找結果 1] 視窗中。 您可以在 [尋找結果 1] 視窗中，按兩下各個項目來瀏覽搜尋相符項目。 若要在新視窗中檢視搜尋結果，請選取 **[顯示在 [尋找結果 2] 視窗]** 。  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>跨多個檔案或資料夾取代  
  
1.  在 **[編輯]** 功能表上，指向 **[尋找和取代]** ，再按一下 **[檔案中取代]** 。  
  
2.  在 **[尋找目標]** 文字方塊中，輸入要搜尋的文字。  
  
3.  在 **[取代成]** 方塊中，輸入用來取代搜尋文字的文字。  
  
4.  在 **[查詢]** 清單中，按一下 **[所有開啟的文件]** 、 **[目前的專案]** 或 **[整個方案]** ，或輸入目錄路徑。  
  
5.  按一下 **[取代]** 來利用 **[取代成]** 方塊中的文字取代目前的搜尋相符項目。 您可以按一下 **[尋找下一個]** 來略過單一相符項目，或按一下 **[略過檔案]** 來略過整個檔案。  
  
     \- 或 -  
  
     選擇 **[取代全部]** 來利用 **[取代成]** 方塊中的文字取代所有搜尋相符項目。 如果您要在其他時候恢復某些取代作業的結果，請選取 **[全部取代後保持已修改檔案為開啟狀態]** 。  
  
    > [!NOTE]  
    >  **[取代全部]** 會取代所有搜尋相符項目，其中包括您已在檔案中，利用 **[略過檔案]** 或 **[尋找下一個]** 來略過的項目。 您只能利用 **[恢復]** 來處理在取代作業之後保持開啟狀態之檔案中的取代項目。  
  
 依預設，取代資訊會出現在 [尋找結果 1] 視窗中。 您可以在 [尋找結果 1] 視窗中，按兩下各個項目來瀏覽取代項目。  
  
## <a name="see-also"></a>另請參閱  
 [搜尋和取代](../../relational-databases/scripting/search-and-replace.md)   
 [以互動方式搜尋文件](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用萬用字元搜尋文字](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
