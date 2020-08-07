---
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
ms.openlocfilehash: b79d4e94126676e128d803176463b314348ed8a1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930919"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>專案設定 (Azure SQL Database )  (SybaseToSQL) 
[Azure SQL Database 專案設定] 可讓您設定要在連接對話方塊中加入 Azure SQL Database 資料庫尾碼，同時也允許在 Azure SQL Database 連接中執行「心跳」機制。  
  
[Azure SQL Database] 窗格可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中取得。  
  
-   使用 [專案設定] 對話方塊，即可設定目前專案的配置選項。 若要存取 Azure SQL Database 設定，請在 [**工具**] 功能表上選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後選取 [ **Azure SQL Database**]。  
  
-   使用 [預設專案設定] 對話方塊，即可設定所有專案的設定選項。 若要存取 Azure SQL Database 設定，請在 [**工具**] 功能表上，選取 [ **DefaultProject 設定**]，按一下左窗格底部的 **[一般**]，然後選取 [ **Azure SQL Database**]。  
  
## <a name="connectivity"></a>連線能力  
**心跳間隔**  
  
指定時間間隔，以用於讓 Azure SQL Database 的連線以「分鐘：秒」格式保持運作的狀態。  
  
**預設值**： ' 4:45 '  
  
值應該以 ' m:ss ' 格式指定 (例如 ' 4:45 ' 或 ' 0:50 ' ) 。  
  
**Azure SQL Database 伺服器尾碼**  
  
指定 Azure SQL Database 伺服器尾碼  
  
**預設值**： ' database.windows.net '。  
  
