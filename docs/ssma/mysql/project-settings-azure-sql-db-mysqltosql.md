---
title: 專案設定 (Azure SQL DB) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e0c16fe617b5808f22f15cdf89af8dc7a1e79898
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311993"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>專案設定 (Azure SQL DB) (MySQLToSQL)
SQL Azure 專案設定可讓您設定 新增連線 對話方塊中，也允許 實作活動訊號機制在 SQL Azure 連接的 SQL Azure 資料庫尾碼。  
  
SQL Azure 窗格位於**專案設定**並**預設專案設定**對話方塊。  
  
-   使用 [專案設定] 對話方塊來設定目前專案的組態選項。 若要存取 SQL Azure 設定 中，在**工具**功能表上，選取**專案設定**，按一下 **一般**在底部的左的窗格中，然後選取**SQLAzure**。  
  
-   使用 [預設專案設定] 對話方塊中設定的所有專案的組態選項。 若要存取 [SQL Azure 設定] 中，在**工具**功能表上，選取**DefaultProject 設定**，選取作為從 SQL Azure 移轉專案類型**移轉目標版本**卸除設定 SQL Azure] 窗格中，按一下 [下存取**一般**底部的左的窗格中，然後選取**SQL Azure**。  
  
## <a name="options"></a>選項。  
  
## <a name="connectivity"></a>連接性  
**活動訊號間隔時間**  
  
指定要用於活動訊號機制，以在維持 SQL Azure 連線的時間間隔 ' 分： 秒數的格式。  
  
**預設值**:' 4:45 '  
  
應該指定的值中是： ss 的格式 (例如，' 4:45 '或' 0:50 ')。  
  
**SQL Azure Server Suffix**  
  
指定 SQL Azure 伺服器的後置詞  
  
**預設值**: 'w'。  
  
