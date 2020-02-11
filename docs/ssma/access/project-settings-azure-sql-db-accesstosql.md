---
title: 專案設定（Azure SQL DB）（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 60140559f94cdeebea935b423fbbeef24bce7a08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929462"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>專案設定（Azure SQL DB）（AccessToSQL）
SQL Azure 專案設定可讓您設定要在連接對話方塊中新增的 SQL Azure 資料庫尾碼，同時也允許在 SQL Azure 連線中執行「心跳」機制。  
  
[SQL Azure] 窗格可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中取得。  
  
-   使用 [專案設定] 對話方塊，即可設定目前專案的配置選項。 若要存取 SQL Azure 設定，請在 [**工具**] 功能表上選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後選取 [ **SQL Azure**]。  
  
-   使用 [預設專案設定] 對話方塊，即可設定所有專案的設定選項。 若要存取 SQL Azure 設定，請在 [**工具**] 功能表上選取 [ **DefaultProject 設定**]，在 [**遷移目標版本**] 下拉式方塊中選取專案類型為 [sql AZURE]，以存取 [sql azure] 窗格中的設定，按一下左窗格底部的 **[一般**]，然後選取 [ **SQL Azure**]。  
  
## <a name="options"></a>選項。  
  
## <a name="connectivity"></a>連線能力  
**心跳間隔**  
  
指定時間間隔，以用於讓 SQL Azure 連線以「分鐘：秒」格式保持運作的狀態。  
  
**預設值**： ' 4:45 '  
  
此值應以 ' m:ss ' 格式指定（例如 ' 4:45 ' 或 ' 0:50 '）。  
  
**SQL Azure 伺服器尾碼**  
  
指定 SQL Azure 伺服器尾碼  
  
**預設值**： ' database.windows.net '。  
  
