---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: 在 SSMS 中使用範本的教學課程。 執行個體時提供 SQL Server 登入。
keywords: SQL Server, SSMS, SQL Server Management Studio, 範本
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: a01586f4ab3d002e33b7679f6fe2e5a165f260e1
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>教學課程：使用 SQL Server Management Studio 中的範本
本教學課程將介紹 SQL Server Management Studio (SSMS) 中可用的預先建立 Transact-SQL (T-SQL) 範本。 在本文中，您將學會如何：

> [!div class="checklist"]
> * 使用範本瀏覽器產生 T-SQL 指令碼
> * 編輯現有範本 
> * 在磁碟上找出範本
> * 建立新的範本
   

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 存取權。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。

 

## <a name="using-the-template-browser"></a>使用範本瀏覽器
在本節中，您將學習如何尋找及使用 [範本瀏覽器]。 

1. 啟動 SQL Server Management Studio。
2. 從 [檢視] 功能表 > [範本瀏覽器] (Ctrl + Alt + T)： 

    ![範本瀏覽器](media/templates-ssms/templatebrowser.png)
    - 您也可以在 [範本瀏覽器] 底部查看最近使用過的範本。

3. 展開您感興趣的節點 > 以滑鼠右鍵按一下 [範本] > [開啟]：

    ![開啟範本](media/templates-ssms/opentemplate.png)
    - 按兩下範本也會有相同的效果。

4. 這會啟動已填入 T-SQL 的新查詢視窗。 
5. 修改範本以符合您需求，然後 [執行] 查詢：
    
    ![建立資料庫範本](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>編輯現有範本
您也可以在 [範本瀏覽器] 內編輯現有範本。  

1. 在 [範本瀏覽器] 中找出感興趣的範本。
2. 以滑鼠右鍵按一下範本 > [編輯]：

    ![編輯範本](media/templates-ssms/edittemplate.png)

3. 請在開啟的查詢視窗中進行所需變更。
4. 前往 [檔案] > [儲存] (Ctrl + S) 以儲存範本。
5. 關閉查詢視窗。
6. 重新開啟已儲存的範本 > 您的新編輯應該會在那裡。
 

## <a name="locate-the-templates-on-disk"></a>在磁碟上找出範本
開啟範本之後，您就可以在磁碟上找到。

1. 在 [範本瀏覽器] > [編輯] 中選取範本。
2. 以滑鼠右鍵按一下 [查詢標題] > [開啟收納資料夾]。 這應該會在瀏覽器上開啟範本儲存在磁碟上的位置： 

    ![在磁碟上的範本](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>建立新的範本
在 [範本瀏覽器] 中，您也可以建立新範本。 這些步驟將教您建立新的資料夾，然後在該資料夾內建立一個新範本。 不過，透過這些步驟，您也可以在現有資料夾中建立自訂範本。 

1. 開啟 [範本瀏覽器]。
2. 以滑鼠右鍵按一下 [SQL Server 範本] > [新增] > [資料夾]。
3. 將此資料夾命名為**自訂範本**：

    ![建立自訂範本](media/templates-ssms/creatingcustomtemplate.png)

4. 以滑鼠右鍵按一下新建立的 [自訂範本] 資料夾 > [新增] > [範本] > 為您的範本命名：
 
    ![建立自訂範本](media/templates-ssms/createnewtemplate.png)
   
5. 以滑鼠右鍵按一下您剛才建立的範本 > [編輯]。 這會開啟 [新增查詢視窗]。
6. 鍵入您想要儲存的 T-SQL 的文字。 
7. 前往 [檔案] 功能表 > [儲存] 以儲存檔案。
8. 關閉現有 [查詢視窗] 並開啟新的自訂範本。 

    

## <a name="next-steps"></a>後續步驟
下一篇文章將使用 SQL Server Management Studio 來提供一些其他祕訣和技巧。 

請前往下一篇文章來進一步了解
> [!div class="nextstepaction"]
> [按鈕](ssms-tricks.md)
