---
title: 專案設定（Azure SQL DB）（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176230"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>專案設定 (Azure SQL DB) (SybaseToSQL)
Azure SQL DB 專案設定可讓您設定要在連接對話方塊中新增的 Azure SQL DB 資料庫尾碼，同時也允許在 Azure SQL DB 連線中執行「檢測」機制。  
  
[**專案設定**] 和 [**預設專案設定**] 對話方塊中提供 [Azure SQL DB] 窗格。  
  
-   使用 [專案設定] 對話方塊，即可設定目前專案的配置選項。 若要存取 Azure SQL DB 設定，請在 [**工具**] 功能表上選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後選取 [ **Azure SQL DB**]。  
  
-   使用 [預設專案設定] 對話方塊，即可設定所有專案的設定選項。 若要存取 Azure SQL DB 設定，請在 [**工具**] 功能表上，選取 [ **DefaultProject 設定**]，按一下左窗格底部的 **[一般**]，然後選取 [ **Azure SQL DB**]。  
  
## <a name="connectivity"></a>連線能力  
**心跳間隔**  
  
指定時間間隔，以用於讓 Azure SQL DB 連線以「分鐘：秒」格式保持運作的心跳機制。  
  
**預設值**： ' 4:45 '  
  
此值應以 ' m:ss ' 格式指定（例如 ' 4:45 ' 或 ' 0:50 '）。  
  
**Azure SQL DB 伺服器尾碼**  
  
指定 Azure SQL DB 伺服器尾碼  
  
**預設值**： ' database.windows.net '。  
  
