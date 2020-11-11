---
description: '從 [尋找及取代] 視窗啟用複製的因應措施 '
title: 啟用從 [尋找及取代] 視窗複製
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: seo-lt-2019
ms.date: 11/03/2020
ms.openlocfilehash: ea5ae3f9fa941e723d3bdf10de0ec900310cc28d
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328772"
---
# <a name="workaround-to-enable-copying-from-find-and-replace-window"></a>從 [尋找及取代] 視窗啟用複製的因應措施

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

您必須解決一個問題，才能從 [尋找及取代] 視窗啟用複製。  如果發現在 SQL Server Management Studio 中無法從 [尋找及取代] 視窗進行複製，請遵循下面的[因應措施](#workaround)。

## <a name="error-message"></a>錯誤訊息

當在 SQL Server Management Studio 中嘗試從 [尋找及取代] 視窗複製文字時，會收到錯誤訊息。

> 無法從其他檔案專案剪下或複製未儲存的文件至剪貼簿。 在剪下或複製未儲存的文件之前，您必須先進行儲存。

![錯誤對話方塊：無法從其他檔案專案剪下或複製未儲存的文件至剪貼簿。 在剪下或複製未儲存的文件之前，您必須先進行儲存](../media/troubleshoot/unable-copy-find-replace-window.png)

## <a name="workaround"></a>因應措施

若要從 [尋找及取代] 視窗啟用複製文字，請遵循下列步驟：

1. 在 [工具] 功能表中，開啟 [選項]。

2. 在 [環境] > [文件] 下，取消核取 [在方案總管中顯示其他檔案] 項目

3. 關閉並重新開啟 SQL Server Management Studio

![[選項] 視窗，其中已取消核取 [在方案總管中顯示其他檔案]](../media/troubleshoot/fix-copy-find-replace-window.png)

