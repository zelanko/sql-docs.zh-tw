---
title: 使用 SQL Server Management Studio 中的範本
description: 在 SSMS 中使用範本的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio, 範本
author: MashaMSFT
ms.author: mathoma
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: jroth
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: a634a106704cebd91ce74910de17166c85c6c4de
ms.sourcegitcommit: 4181429ada1169871c2f4d73d18d2ba013007501
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866264"
---
# <a name="use-templates-in-sql-server-management-studio"></a>使用 SQL Server Management Studio 中的範本

本教學課程將介紹 SQL Server Management Studio (SSMS) 中可用的預先建立 Transact-SQL (T-SQL) 範本。 在此文章中，您將學會如何：

## <a name="prerequisites"></a>Prerequisites

若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 存取權。

* 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

* 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

## <a name="use-template-browser"></a>使用範本瀏覽器

在本節中，您將學習如何尋找及使用範本瀏覽器。

1. 開啟 SQL Server Management Studio。

2. 在 [檢視]  功能表中，選取 [範本瀏覽器]  (Ctrl+Alt+T)：

    ![開啟範本瀏覽器](media/templates-ssms/templatebrowser.png)

    您可以在範本瀏覽器底部查看最近使用過的範本。

3. 展開您感興趣的節點。 以滑鼠右鍵按一下範本，然後選取 [開啟]  。

    ![開啟範本](media/templates-ssms/opentemplate.png)

    您也可以按兩下範本名稱以開啟它。

4. 隨即開啟 [新增查詢] 視窗。 已填入 T-SQL 指令碼。

5. 修改範本以符合您的需求，然後選取 [執行]  來執行查詢：

    ![建立資料庫範本](media/templates-ssms/createdbtemplate.png)

## <a name="edit-an-existing-template"></a>編輯現有範本

您也可以在範本瀏覽器內編輯現有範本。  

1. 在範本瀏覽器中，移至您想要使用的範本。

2. 以滑鼠右鍵按一下範本，然後選取 [編輯]  ：

    ![編輯範本](media/templates-ssms/edittemplate.png)

3. 在開啟的查詢視窗中，進行您想要的變更。

4. 選取 [檔案]   > [儲存]  (Ctrl + S) 以儲存範本。

5. 關閉查詢視窗。

6. 重新開啟範本。 您的編輯應該會出現。

## <a name="locate-templates-on-disk"></a>在磁碟上找出範本

開啟範本時，您可以找出磁碟上的範本。

1. 在範本瀏覽器中選取範本，然後選取 [編輯]  。

2. 以滑鼠右鍵按一下 [查詢標題]  ，然後選取 [開啟所屬資料夾]  。 總管應該會開啟範本儲存在磁碟上的位置： 

   ![磁碟上的範本](media/templates-ssms/templatesondisk.png)
  
## <a name="create-a-new-template"></a>建立新的範本

您也可以在範本瀏覽器中建立新的範本。 下列步驟示範如何建立新的資料夾，然後在該資料夾內建立一個新範本。 您也可以使用這些步驟，在現有的資料夾中建立自訂範本。 

1. 開啟範本瀏覽器。

2. 以滑鼠右鍵按一下 [SQL Server 範本]  ，然後選取 [新增]   > [資料夾]  。

3. 將此資料夾命名為**自訂範本**：

    ![建立自訂範本資料夾](media/templates-ssms/creatingcustomtemplate.png)

4. 以滑鼠右鍵按一下新建立的 [自訂範本] 資料夾，然後選取 [新增]   > [範本]  。 輸入您的範本名稱：

    ![建立自訂範本](media/templates-ssms/createnewtemplate.png)

5. 以滑鼠右鍵按一下您建立的範本，然後選取 [編輯]  。 隨即開啟 [新增查詢] 視窗。

6. 輸入您想要儲存的 T-SQL 文字。

7. 在 [檔案]  功能表中，選取 [儲存]  。

8. 關閉現有查詢視窗，然後開啟您的新自訂範本。

## <a name="next-steps"></a>後續步驟

熟悉 SSMS 的最佳方式是實際練習。 這些「教學課程」  與「操作方式」  文章可協助您使用 SSMS 內所提供的各種功能。  這些文章會告訴您如何管理 SSMS 的元件及如何尋找您經常使用的功能。

* [連線至執行個體並對其進行查詢](../tutorials/connect-query-sql-server.md)
* [指令碼](../tutorials/scripting-ssms.md)
* [SSMS 組態](../tutorials/ssms-configuration.md)
* [使用 SSMS 的其他提示與訣竅](../tutorials/ssms-tricks.md)