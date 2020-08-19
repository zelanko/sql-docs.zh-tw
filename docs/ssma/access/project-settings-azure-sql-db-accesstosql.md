---
description: '專案設定 (Azure SQL Database)  (AccessToSQL) '
title: 專案設定 (Azure SQL Database)  (AccessToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9954fe012158526e87bd30512b13eca0314bc00e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418544"
---
# <a name="project-settings-azure-sql-database-accesstosql"></a>專案設定 (Azure SQL Database)  (AccessToSQL) 
SQL Azure 專案設定可讓您設定要在連接對話方塊中新增的 Azure SQL Database 尾碼，也可讓您在 SQL Azure 連線中執行執行的「心跳」機制。  
  
[SQL Azure] 窗格可在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用。  
  
-   使用 [專案設定] 對話方塊，即可設定目前專案的設定選項。 若要存取 SQL Azure 設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後選取 [ **SQL azure**]。  
  
-   使用 [預設專案設定] 對話方塊，即可設定所有專案的設定選項。 若要存取 SQL Azure 設定，請選取 [ **工具** ] 功能表上的 [ **DefaultProject 設定**]，在 [ **遷移目標版本** ] 下拉式方塊中選取 [sql azure] 專案類型，以存取 [sql azure] 窗格中的設定，按一下左窗格底部的 **[一般** ]，然後選取 [ **SQL azure**]。  
  
## <a name="options"></a>選項。  
  
## <a name="connectivity"></a>連線能力  
**心跳間隔**  
  
指定要用於心跳機制的時間間隔，讓 SQL Azure 連線保持在「分鐘：秒」格式的狀態。  
  
**預設值**： ' 4:45 '  
  
值應以 ' m:ss ' 格式指定 (例如 ' 4:45 ' 或 ' 0:50 ' ) 。  
  
**SQL Azure 伺服器尾碼**  
  
指定 SQL Azure 伺服器尾碼  
  
**預設值**： ' database.windows.net '。  
  
