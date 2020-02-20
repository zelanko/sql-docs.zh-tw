---
title: 第 2 課：指定連線資訊 (Reporting Services) | Microsoft Docs
description: 在本課程中，您將定義資料來源；亦即報表從關聯式資料庫或其他來源存取資料所使用的連線資訊。
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d4e12a0322a35e96bd930c4fa6f1f852daf2bdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258457"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 課：指定連線資訊 (Reporting Services)

在第 1 課，您已經將 [!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] 編頁報表加入至 Tutorial 專案。
  
在本課中，您將定義*資料來源*、報表從關聯式資料庫或其他來源存取資料所使用的連線資訊。

針對此報表，您將 AdventureWorks2016 範例資料庫作為資料來源。 本教學課程假設此資料庫位於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 的預設執行個體中，並安裝在本機電腦上。  

## <a name="to-set-up-a-connection"></a>設定連接  

1. 在 [報表資料]  窗格中，選取 [新增]   > [資料來源]  。 如果看不到 [報表資料]  窗格，則選取 [檢視]  功能表 > [報表資料]  。

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    [資料來源屬性]  對話方塊隨即開啟，並顯示 [一般]  區段。

    ![資料來源屬性對話方塊](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. 在 [名稱]  文字方塊中，輸入 "AdventureWorks2016"。

3. 選取 [內嵌連接]  選項按鈕。

4. 在 [類型]  下拉式選項方塊中，選取 [Microsoft SQL Server]。
  
5. 在 [連接字串]  文字方塊，輸入下列字串：

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > 這個連接字串假設 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、報表伺服器和 AdventureWorks2016 資料庫都安裝在本機電腦上。
    >
    >如果假設並不正確，請變更連接字串，並將 "localhost" 取代為您資料庫伺服器/執行個體的名稱。 如果您使用的是 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 或 SQL Server 具名執行個體，您需要修改連接字串，以包含執行個體資訊。 例如：
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > 如需有關連接字串的詳細資訊，您可以參閱以下的 `See also` 章節。

6. 選取 [認證]  索引標籤，並在 [變更用來連接資料來源的認證]  區段底下，選取 [使用 Windows 驗證 (整合式安全性)]  選項按鈕。

7. 選取 [確定]  以完成程序。

報表設計師會將資料來源 AdventureWorks2016 新增至 [報表資料]  窗格。

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>後續步驟

在本課中，您已成功定義與 AdventureWorks2016 範例資料庫的連線。 繼續進行[第 3 課：定義資料表報表的資料集 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md) 以定義報表的資料集。

## <a name="see-also"></a>另請參閱

[建立資料連接字串 - 報表產生器及 SSRS](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
