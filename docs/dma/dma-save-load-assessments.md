---
title: 使用 Data Migration Assistant 儲存和載入評量
description: 瞭解如何使用 Data Migration Assistant 來儲存和載入評量。
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 02a6d49202ad2607d862246eee232e599788244a
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885855"
---
# <a name="save-and-load-assessments-with-data-migration-assistant"></a>使用 Data Migration Assistant 儲存和載入評量

下列逐步指示可協助您使用 Data Migration Assistant 5.0 版或更新版本，將資料庫評估儲存至檔案，然後從檔案載入評量。

> [!NOTE]
> 除了載入使用最新版本的 DMA 儲存的評量之外，使用者也可以利用這項功能來載入從舊版 Data Migration Assistant 匯出為 json 檔案的評量，以在5.0 版和更新版本中查看結果。

## <a name="saving-an-assessment-to-a-file"></a>將評量儲存至檔案

1. 使用 Data Migration Assistant 執行評估之後，請選取 [**儲存評估**]。

   ![開啟 [儲存評估] 對話方塊](../dma/media/dma-save-load-assessments/dma-open-save-dialog.png)

   標準**儲存 ...** 對話方塊隨即出現。

   > [!NOTE]
   > 如需如何在 Data Migration Assistant 中執行評量的詳細資訊，請參閱[使用 Data Migration Assistant 執行 SQL Server 遷移評估](../dma/dma-assesssqlonprem.md)一文。

2. 指定檔案名，然後選取 [**儲存**]。

   ![命名及儲存評估檔案](../dma/media/dma-save-load-assessments/dma-name-save-assessment.png)

## <a name="loading-an-assessment-saved-to-a-file"></a>載入儲存至檔案的評量

1. 若要載入您先前儲存至檔案的評量，請啟動 Data Migration Assistant，然後在 [**所有評**量] 索引標籤上，選取 [**負載評定**]。

   ![開啟 [負載評估] 對話方塊](../dma/media/dma-save-load-assessments/dma-open-load-dialog.png)

2. 流覽至您想要載入的已儲存評估檔案，選取該檔案，然後選取 [**開啟**]。

   ![開啟評估檔案](../dma/media/dma-save-load-assessments/dma-open-assessment.png)

   您所載入評量的專案會出現在 [**所有評**量] 索引標籤上。

   ![顯示評量專案](../dma/media/dma-save-load-assessments/dma-display-assessment-entry.png)

3. 選取 [評估] 專案，然後選取 [**開啟評估**]。

   ![開啟評量詳細資料](../dma/media/dma-save-load-assessments/dma-open-assessment-detail.png)

   Data Migration Assistant 現在會顯示您先前執行之評量的詳細資料。

   ![顯示評量詳細資料](../dma/media/dma-save-load-assessments/dma-display-assessment-detail.png)
