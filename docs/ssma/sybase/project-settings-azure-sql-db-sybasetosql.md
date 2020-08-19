---
description: '專案設定 (Azure SQL Database )  (SybaseToSQL) '
title: 專案設定 (Azure SQL Database )  (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 39a099eb243d767d18402bcd6baeb6280dbeaad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418274"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>專案設定 (Azure SQL Database )  (SybaseToSQL) 
Azure SQL Database 專案設定可讓您設定要在連接對話方塊中加入的 Azure SQL Database 資料庫尾碼，也可讓您在 Azure SQL Database 連接中執行資料庫尾碼。  
  
您可以在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用 [Azure SQL Database] 窗格。  
  
-   使用 [專案設定] 對話方塊，即可設定目前專案的設定選項。 若要存取 Azure SQL Database 設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後選取 [ **Azure SQL Database**]。  
  
-   使用 [預設專案設定] 對話方塊，即可設定所有專案的設定選項。 若要存取 Azure SQL Database 設定，請在 [ **工具** ] 功能表上選取 [ **DefaultProject 設定**]，按一下左窗格底部的 **[一般** ]，然後選取 [ **Azure SQL Database**]。  
  
## <a name="connectivity"></a>連線能力  
**心跳間隔**  
  
指定要用於心跳機制的時間間隔，以在「分鐘：秒」格式保持 Azure SQL Database 連接保持運作。  
  
**預設值**： ' 4:45 '  
  
值應以 ' m:ss ' 格式指定 (例如 ' 4:45 ' 或 ' 0:50 ' ) 。  
  
**Azure SQL Database 伺服器尾碼**  
  
指定 Azure SQL Database 伺服器尾碼  
  
**預設值**： ' database.windows.net '。  
  
